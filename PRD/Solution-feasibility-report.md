# Đánh giá phương án và mức độ khả thi

31/10/2026. Đây là đánh giá của tác giả dựa trên artifact, research công khai trong repo và kiểm tra UI; không phải audit Alipay/Tencent hoặc validation với dữ liệu Shopee thật.

## Kết luận và điểm số

**Đúng hướng nếu định vị là agent hỗ trợ điều tra/triage có giới hạn. Chưa đủ bằng chứng để tuyên bố hệ thống AML tự chủ hoặc đã giảm false positive.** Chấp thuận tiếp tục MVP có điều kiện; chưa chấp thuận vận hành trên giao dịch thật.

Điểm là nhận định thiết kế theo thang 10, không phải xác suất thành công hay điểm ban giám khảo. Không cộng thành một điểm trung bình dễ gây hiểu nhầm.

| Hạng mục | Điểm | Cơ sở |
|---|---:|---|
| Phù hợp công việc analyst | 7/10 | Có bằng chứng, phản chứng, disposition và audit; chưa phỏng vấn analyst thật |
| UX bản đồ TP.HCM | 8/10 | Map chi tiết, navigation riêng, ba vòng UI checks; chưa usability test với người dùng |
| Khả thi MVP kỹ thuật | 8/10 | Engine đã có theo thông tin người dùng; có thể thêm worker/tool đọc; integration contract chưa xác minh |
| Phù hợp Autonomous & Adaptive AI hiện tại | 3/10 | Hiện chỉ là wireframe/scripted state, chưa có runtime agent |
| Tiềm năng phù hợp track sau implementation | 8/10 | Agent tự chọn bước, bounded recovery, escalation và tested adaptation có thể demo được |
| Bằng chứng giảm false positive | 1/10 | Số liệu 20→12 là hardcoded, không phải kết quả đo |
| Sẵn sàng production | 2/10 | Chưa có auth, backend audit, eval thực, persistent data hoặc operational controls |

## Đối chiếu Alipay và WeChat Pay

Đọc research trong repo: [Alipay findings](../research/alipay-wechat-bnpl/alipay-findings.md), [WeChat findings](../research/alipay-wechat-bnpl/wechat-findings.md). Các mã nguồn dưới đây được kế thừa từ source register của research; không tuyên bố đã fetch lại tất cả nguồn trong lượt này.

| Bằng chứng research | Ý nghĩa với phương án | Không được suy ra |
|---|---|---|
| Alipay A4–A5 / S3: identity/business verification, risk information và quyền điều tra/hạn chế thanh toán | Merchant context và điều tra có căn cứ là đúng hướng | Đây là kiến trúc LLM/GNN của Huabei hoặc hiệu quả đã audit |
| Ant A7 / S4: company release về AML framework, indicators và automation cấp tập đoàn | Cần governance và indicator/version management | Mọi capability có trong Huabei hoặc LLM tự quyết định báo cáo |
| Fenfu W-C2 / W1: đánh giá giao dịch thời gian thực | Detector cần riêng khỏi investigation async | LLM phù hợp latency quyết định thanh toán |
| Fenfu W-C5 / W2: mục đích xử lý identity/transaction/device/network data | Những entity đề xuất hợp lý để mô phỏng có nguồn bằng chứng | Mọi feature được dùng trong mọi quyết định |
| Tencent W7–W8: AML governance, monitoring, independent testing | Giữ audit, đánh giá và kiểm soát thay đổi | Internal investigator flow hoặc model weights được công bố |
| Research không có false-positive/false-negative metrics sản phẩm | Phải tự đánh giá baseline/candidate | Có thể mượn mức hiệu quả của đối thủ để validate demo |

Research cũng cảnh báo: wallet, lender và payment operator không đồng nhất; credit risk khác fraud và AML. Authorized borrowing không phải sham-transaction cash-out. Không dùng delinquency, IP xa hoặc device chung làm kết luận laundering. Quy định/contract Trung Quốc không tự chuyển thành nghĩa vụ của ShopeePay ở Việt Nam.

**Kiểm tra nguồn mới trong lượt này:** thử mở lại S3 trên domain Alipay bị timeout; do đó các nhận định S3 ở trên dựa vào research đã lưu, không được gọi là reverified. OSM tile policy đã mở và đọc lại thành công. Research WeChat W1/W2/W7/W8 và Ant S4 giữ nguyên mức tin cậy và giới hạn của tài liệu gốc.

## Chấm phần validation hiện tại

Đã validate: rendering map, menu, filter, draft, test-before-apply UI, rollback giả lập và lỗi tile. Chưa validate: extraction đúng, multi-hop reasoning, detection recall, precision, tốc độ điều tra thực, giảm công việc analyst hoặc tác động tài chính.

Ba vòng kiểm tra UI là bằng chứng chất lượng giao diện, không phải ba vòng kiểm định fraud model. Map đẹp cũng không chứng minh tín hiệu địa lý có giá trị dự báo.

## Thử nghiệm cần làm để chứng minh solution

1. **Đóng băng fixture và ground truth:** tối thiểu một tập discovery nhỏ và một tập held-out riêng; có fraud ring, public IP hợp lệ, dữ liệu thiếu, tool timeout, adversarial merchant memo và lawful credit disbursement. Ghi nhãn adjudicated/uncertain riêng. Kích thước hackathon chỉ đủ chứng minh workflow.
2. **Ba baseline cùng dữ liệu:** A detector/rules hiện có; B rules + evidence bundle cố định; C rules + agent điều tra. So sánh cùng budget và policy routing để biết lợi ích đến từ agent hay chỉ từ enrichment.
3. **Ablation:** bỏ precedent retrieval hoặc graph expansion và chạy lại. Nếu không cải thiện đủ, bỏ cơ chế đó khỏi MVP.
4. **Metric đúng mẫu số:** false-positive rate = legitimate escalated / all legitimate; precision = fraud escalated / all escalated; recall = fraud escalated / all fraud. Báo missed fraud, unresolved cases, review time, tool failure, token usage và end-to-end latency. Không loại incomplete cases khỏi mẫu số mà không công bố.
5. **Gate đề xuất trước khi chạy:** không có evidence ID bịa; không có tool/write vượt quyền; mọi critical fixture được route đúng; candidate không tăng missed fraud trên held-out và giảm false escalation. Gate này không chứng nhận production safety. Báo raw counts và số mẫu; không tuyên bố chắc chắn về mức giảm từ tập nhỏ.
6. **Human test:** 2–3 analyst nếu tiếp cận được; nếu teammate thì ghi proxy. Cho tìm và kết luận một case bằng list-first và map-first, luân phiên thứ tự. Đo thời gian gồm kiểm tra/chỉnh sửa và lỗi kết luận, không chỉ click count.

## Phản biện và scope decision

- Map có giá trị cho use case địa lý nhưng dễ làm người xem đánh giá quá mức IP location. Giữ list và provenance; thử nghiệm xem map có thật sự nhanh hơn list.
- Trained GNN và streaming feature store có thể vượt ngân sách hackathon. Trước hết dùng graph queries với dữ liệu có timestamp; chỉ thêm khi baseline chứng minh nhu cầu.
- Learning từ một analyst click có thể khuếch đại lỗi hoặc tạo lỗ hổng suppression. Dùng precedent có scope và review; tránh blanket allowlist; giữ stronger device/velocity signals.
- Chỉ TP.HCM là phạm vi UX/demo, không chứng minh fraud ring dừng ở địa giới. Backend không nên cắt evidence ngoài thành phố; hiển thị out-of-area evidence trong hồ sơ dù không mở rộng map.
- Tuyên bố “giảm 40% false positive” hiện không hợp lệ. Có thể nói “demo minh họa quy trình kiểm tra mức giảm”, đến khi có eval log thật.

## Go / no-go

**GO:** xây một vertical slice nhận alert → đọc evidence → agent chọn next check → validator/router → case → analyst feedback → held-out evaluation → approval/rollback. Giữ mock data và cấm side effect lên thanh toán.

**NO-GO hiện tại:** production deployment, tự động freeze/decline, AML regulatory filing, tuyên bố detection performance hoặc công bố kiến trúc này như cơ chế nội bộ Alipay/Tencent.

Bước tiếp theo nên là fixture + baseline + một worker, không phải thêm dashboard hoặc nhiều agent. Xem [implementation design](Implementation-design.md) và diagram trong [README gốc](../README.md).
