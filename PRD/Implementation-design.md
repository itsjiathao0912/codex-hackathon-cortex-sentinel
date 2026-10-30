> Current specification: [English PRD](PRD.md) and [architecture rationale](Architecture-rationale.md). This earlier design is supporting context; PRD state machines, budgets and acceptance criteria take precedence.

# Thiết kế triển khai — map TP.HCM và AI triage

31/10/2026. Đề xuất kỹ thuật, không phải mô tả backend đã chạy.

## 1. Bản đồ

Giữ Leaflet 1.9.4 cho MVP: thư viện hiện đã nằm trong `assets`, có license; rendering đường phố và điểm hồ sơ đã hoạt động. Không cần MapLibre/3D/GNN để vẽ map. Không vẽ đường nối theo yêu cầu người dùng.

Tách UI thành MapPage, ConfigurationPage, CasesPage, AuditPage; shared store giữ configurationId, selectedCaseId, period và trạng thái draft. MapPage sở hữu một map instance, hủy listeners khi unmount; invalidateSize khi mở lại và fitBounds theo tập điểm có dữ liệu. Không tái tạo map trên mỗi lần cập nhật hồ sơ.

**Map API đề xuất:** `GET /cases?configurationId=&from=&to=&bbox=&cursor=` trả danh sách được phân quyền, pagination và tọa độ được phép hiển thị. Dùng bbox để giảm payload, nhưng quyền truy cập luôn kiểm tra ở server. Queue/case detail là nguồn sự thật; map chỉ là một view.

**Location contract:** caseId, latitude, longitude, locationSource (`merchant_registry`, `ip_estimate`, `synthetic`), observedAt, accuracyRadiusKm hoặc null, confidenceClass và evidenceId. GeoJSON dùng `[longitude, latitude]`; Leaflet dùng `[latitude, longitude]`. Không được tráo thứ tự. Missing coordinates: giữ trong danh sách và ghi Không có vị trí, không gán 0,0 hay trung tâm thành phố. Merchant fallback phải ghi rõ nguồn; không coi là IP/device location.

**Map updates:** MVP dùng polling có backoff; nếu cần SSE, dùng event ID để resume và deduplicate. Cập nhật marker theo caseId thay vì reset pan/zoom. Khi số lượng lớn, cluster marker và truy vấn bbox; không render toàn bộ giao dịch. Dataset hackathon chỉ cần vài chục hồ sơ đã tổng hợp.

**Địa giới:** wireframe hiện giới hạn vùng trung tâm/đô thị TP.HCM bằng bbox, không xác nhận ranh giới hành chính hiện hành. Nếu yêu cầu phủ toàn bộ thành phố, cần nguồn polygon hành chính có ngày hiệu lực, xác minh và version hóa trước khi dùng point-in-polygon.

**Tile provider:** public OSM chỉ dùng demo tương tác vừa phải; production chọn nhà cung cấp có điều khoản tải/traffic phù hợp hoặc self-host. Giữ attribution, browser caching và Referer. Không bulk download/prefetch public tiles. Kiểm thử tự động dùng mock tile response; không pan/zoom hàng loạt để ép tải tile thật. Tile provider thấy vùng viewport, IP mạng và Referer; không gửi case/account IDs hoặc thông tin cá nhân trong URL tile. Nhu cầu riêng tư cao cần provider/phương án self-host được duyệt.

Nguồn chính thức: [Leaflet API](https://leafletjs.com/reference.html), [OSM tile policy](https://operations.osmfoundation.org/policies/tiles/) — policy đã đọc lại trong lần đánh giá này, không có SLA và yêu cầu attribution, cache, Referer.

## 2. AI triage backend

**Ranh giới:** giữ detector hiện có trên luồng transaction; AI worker nhận alert bất đồng bộ. Không đặt LLM trên đường quyết định thanh toán millisecond.

1. Chuẩn hóa alert thành `alertId, eventTime, accountIds, merchantIds, evidenceRefs, ruleVersion`.
2. Queue job với idempotency key từ alertId + investigationVersion. Gom case dựa trên entity/time window có giới hạn; không gom mọi tài khoản chỉ vì cùng IP.
3. Tạo snapshot point-in-time: transaction history, rule signals, relationship edges và precedent chỉ tồn tại trước thời điểm điều tra.
4. Agent được gọi công cụ chỉ đọc: `get_case_evidence`, `get_recent_activity`, `expand_relationships`, `get_location_context`, `retrieve_reviewed_cases`. Server kiểm tra entity scope, time window, max hops và kích thước kết quả.
5. Budget khởi điểm đề xuất: tối đa 8 tool calls, 2 retries/tool và 30 giây/job; phải đo lại trước khi chốt. Tool trả dữ liệu không chứa chỉ dẫn đáng tin; nội dung merchant/memo được xem là untrusted.
6. Output contract: `caseId, assessment, supportingEvidenceIds, counterEvidenceIds, missingEvidence, suggestedPriority, suggestedRoute, policyVersion`. `assessment` gồm suspicious, likely_legitimate, insufficient_evidence. Không dùng confidence do LLM tự khai như xác suất fraud đã hiệu chuẩn.
7. Validator kiểm tra schema, evidence tồn tại/đúng case/đúng snapshot, quyền công cụ và fields bắt buộc. Invalid/refusal/timeout tạo Needs review, không tự clear.
8. Router deterministic áp dụng policy đã duyệt, tạo case/escalation bằng outbox và khóa idempotency để retry không gửi trùng. Ghi delivery status, acknowledgment và backup escalation; không coi việc model đề nghị là đã gửi thành công.
9. Analyst disposition và lý do được lưu riêng với assessment; snapshot bất biến, lưu prompt/model/config version và tool trace ngắn gọn, không yêu cầu private chain-of-thought.

**Persistence đề xuất:** alerts, cases, evidence_snapshots, investigation_runs, analyst_decisions, policy_versions, evaluation_runs, outbox_events. State: queued → investigating → needs_review/escalated → reviewed. Failed jobs giữ nguyên bằng chứng và lý do lỗi. Quyền apply policy tách với quyền đọc; secret API chỉ ở backend.

## 3. Learning có kiểm soát

MVP dùng retrieval các quyết định đã được review và candidate policy có phạm vi; không tự fine-tune sau từng click. Decision labels cần reviewer, lý do và mức xác nhận; suspected fraud chưa phải adjudicated fraud.

Tách ba tập: lịch sử retrieval, development, held-out evaluation. Tách theo thời gian và nhóm liên quan để cùng một fraud ring không rò sang hai tập. Candidate đi qua replay, kiểm tra critical cases, phê duyệt, shadow mode, version và rollback. Không dùng held-out để tune lặp đi lặp lại; thay tập khi đã dùng để chọn model nhiều lần.

## 4. Implementation order và done criteria

| Giai đoạn | Deliverable | Done khi |
|---|---|---|
| A | Case API + fixtures + map | Chọn cấu hình lọc đúng; tọa độ thiếu vẫn có trong list |
| B | Alert queue + read-only tools | Job lặp không tạo case/escalation trùng |
| C | Một agent + validator + router | Tạo evidence-backed case; timeout và invalid output đi review |
| D | Analyst feedback + candidate replay | Quyết định không tự sửa policy; approve/rollback có version |
| E | Eval + demo | Chạy fixture frozen, lưu raw outputs, latency, usage và lỗi |

MVP không thêm feature store mới hoặc trained GNN nếu chưa chứng minh chúng cải thiện baseline. Quan hệ có thể truy vấn trực tiếp từ bảng/index cho fixture nhỏ; GNN là thí nghiệm sau, không là điều kiện triển khai.
