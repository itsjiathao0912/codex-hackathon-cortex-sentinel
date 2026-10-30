# Cortex Sentinel — luồng MVP TP.HCM

Ngày: 31/10/2026. Trạng thái: đề xuất UX và wireframe; chưa phải BRD/PRD được chốt.

## Thay đổi theo yêu cầu

Chỉ theo dõi khu vực TP.HCM, có đường phố và địa danh thật. Bỏ bản đồ thế giới, các đường nối và kiểu gom mọi chức năng vào một màn hình. Dùng menu dọc với Bản đồ, Cấu hình, Hồ sơ rủi ro, Nhật ký. Bỏ bảng màu xanh, chuyển sang cam đất, nâu, xám ấm và nền sáng.

## Người dùng và mục tiêu

Chuyên viên risk/fraud của ShopeePay và ShopeePayLater. Engine hiện có tiếp tục ingest dữ liệu và xử lý use case. Lớp AI đề xuất điều tra, gom bằng chứng và chuyển cấp trong phạm vi được cho phép; phản hồi chuyên viên tạo đề xuất điều chỉnh được kiểm tra và phê duyệt.

## 1. Bản đồ

Mở trực tiếp vào khu vực trung tâm TP.HCM. Chọn một trong ba cấu hình mẫu: Giao dịch tại merchant, Bất thường vị trí, Thiết bị dùng chung. Chọn khoảng thời gian 1 giờ, 24 giờ hoặc 7 ngày.

Map dùng Leaflet và tile OpenStreetMap, giữ attribution. Nền địa lý chuyển sang tông trung tính. Chỉ có các marker đánh số; không có polyline, vòng IP hoặc dây liên kết. Đổi cấu hình tự căn khung để nhìn thấy các hồ sơ. Người dùng có thể phóng to/thu nhỏ, kéo map và về trung tâm. Phạm vi kéo/zoom được giới hạn quanh TP.HCM; không có chế độ thế giới.

Click marker hoặc thẻ hồ sơ để xem bằng chứng, điểm chưa chắc chắn và nguồn vị trí. Marker minh họa các khu vực Bến Thành, Nguyễn Huệ, Thủ Thiêm, Tân Sơn Nhất, Văn Thánh và Chợ Lớn; không ngụ ý các địa điểm thật này có gian lận. Các tọa độ chỉ là dữ liệu demo.

Nút Chỉnh cấu hình mở đúng cấu hình đó trong mục Cấu hình. Không có wizard bắt buộc trước khi xem map.

## 2. Cấu hình

Trang riêng với danh sách cấu hình bên trái và form bên phải. Các trường: tên, sản phẩm, mức chuyển cấp, độ sâu quan hệ, chênh lệch vị trí từ 1–100 km (số nguyên), nhóm nhận cảnh báo.

Luồng: chỉnh → Kiểm tra giả lập → xem kết quả tại chỗ → Áp dụng cấu hình. Thay đổi sau khi kiểm tra làm vô hiệu kết quả và nút Áp dụng. Áp dụng tăng phiên bản và ghi nhật ký. Hủy thay đổi khôi phục cấu hình đã áp dụng. Bản nháp được giữ khi chuyển mục trong phiên; không persist qua reload.

Địa chỉ, số lượng và cấu hình không phải bằng chứng hiệu quả mô hình. Replay trong wireframe là kết quả cố định, không tính lại từ giao dịch.

## 3. Hồ sơ rủi ro

Danh sách hồ sơ của cấu hình đang chọn, độc lập với thời gian lọc của map. Click mã hồ sơ để mở detail cùng trang. Ghi một trong ba kết luận: Xác nhận gian lận, Hoạt động hợp lệ, Chưa đủ bằng chứng; bắt buộc nhập lý do.

Bản nháp kết luận giữ khi đổi mục hoặc tạm dừng. Kết luận đã lưu cập nhật cả map và bảng. Chưa đủ bằng chứng không được hiểu là hồ sơ đã an toàn. Wireframe không có workflow đóng/mở lại hoàn chỉnh.

Với C-105, kết luận Hoạt động hợp lệ cho phép xem đề xuất giảm trọng số IP dùng chung, chỉ với M-031 và điều kiện thiết bị/nhịp giao dịch độc lập. So sánh giả lập: chuyển nhầm 20 → 12/80; phát hiện 18/20 và bỏ sót 2/20 không đổi. Cần phê duyệt; có hoàn tác. Đây không phải học mô hình thực tế.

## 4. Nhật ký

Trang riêng chứa sự kiện trong phiên: thay đổi trạng thái agent, áp dụng cấu hình, lưu kết luận và phê duyệt/hoàn tác điều chỉnh. Hiện là bộ nhớ trình duyệt, không phải audit backend bền vững.

## Lỗi và quyền tự chủ

- Tile không tải được: thông báo rõ, có nút thử lại; danh sách hồ sơ vẫn hoạt động.
- C-202 minh họa tra cứu IP lỗi; dùng vị trí merchant và ghi rõ thiếu bằng chứng.
- Tạm dừng: trạng thái đổi, giữ dữ liệu và bản nháp. Chỉ mô phỏng việc xếp hàng công việc mới.
- Agent đề xuất được điều tra, gom hồ sơ và chuyển cấp. Không tự chặn tiền, khóa tài khoản hoặc gửi báo cáo pháp lý.
- Các thay đổi policy và điều chỉnh học từ chuyên viên cần kiểm tra và phê duyệt.

## Phạm vi thực tế của artifact

Ba cấu hình, sáu hồ sơ giả lập trong TP.HCM, bốn mục điều hướng, map đường phố có zoom/pan, chỉnh cấu hình/phiên bản, quyết định có lý do, nhật ký, cải tiến giả lập và rollback. Không có AI API, GNN, live stream, tài khoản thật, thông báo thật, persist backend hoặc đánh giá thống kê.

Trước khi chốt BRD/PRD: xác nhận hợp đồng với engine, schema, tiêu chí chuyển cấp, người phê duyệt, vòng đời hồ sơ, dữ liệu nhãn và tiêu chí đánh giá thực tế. Thiết kế này thay thế các mô tả map thế giới và single-workspace trước đó.
