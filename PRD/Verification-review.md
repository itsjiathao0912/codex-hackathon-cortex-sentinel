# Kiểm tra ba vòng — phiên bản TP.HCM

Ngày: 31/10/2026. Tác giả tự review bằng browser automation và kiểm tra screenshot; không phải đánh giá độc lập hoặc kiểm định hệ thống fraud thật.

## Vòng 1 — Luồng và yêu cầu

Chín kiểm tra đạt: street tiles tải được; không có đường nối; marker xuất hiện; trang Cấu hình tách riêng; test mở khóa áp dụng; phiên bản tăng; tên cấu hình đồng bộ về map; mục Hồ sơ mở được; nhật ký có sự kiện áp dụng.

Kết luận: yêu cầu cấu trúc mới được đáp ứng; không còn wizard hay chế độ thế giới.

## Vòng 2 — Bố cục và địa lý

Xem screenshot desktop và mobile. Không tràn ngang ở 1600, 1024, 768, 390 và 320 px. Desktop dùng menu dọc; màn hình nhỏ chuyển menu thành thanh gọn. Nền map và UI dùng màu trung tính/cam đất, không dùng xanh làm bảng màu chủ đạo.

Phát hiện: đổi cấu hình trên điện thoại có thể đặt cả hai điểm ngoài khung nhìn. Sửa bằng fitBounds có padding, zoom tối đa 14 khi đổi cấu hình và quay lại map. Retest: cả C-201 và C-202 nằm trong khung. Bỏ biểu tượng màu mặc định khỏi prefix Leaflet, vẫn giữ attribution văn bản và liên kết.

## Vòng 3 — Biên và lỗi mạng

Mười hai kiểm tra đạt: giữ draft quyết định qua chuyển mục; giữ draft cấu hình; chặn khoảng cách thập phân; giá trị hợp lệ chạy test; chỉnh lại bắt retest; hủy khôi phục; phê duyệt điều chỉnh; hoàn tác; pause; báo lỗi tile; hồ sơ dùng được khi tile bị chặn; retry tải lại map.

Cố ý chặn request tile trong trình duyệt để tái hiện mất bản đồ rồi bỏ chặn và thử lại. Network errors trong thử nghiệm này là có chủ đích. Không ghi nhận lỗi JavaScript runtime trong lần kiểm tra.

## Tự đánh giá

- Đúng định hướng: tốt — TP.HCM chi tiết, không dây nối, menu mục riêng, màu cam đất.
- Desktop: phù hợp demo; map lớn và detail đọc được.
- Mobile: hoạt động, không tràn ngang; vẫn cần cuộn để đọc hồ sơ.
- Chất lượng dữ liệu/mô hình: chưa đánh giá vì mọi hoạt động là giả lập.
- Sẵn sàng production: chưa; thiếu backend, authentication, lưu bền vững, AI thật và đánh giá model.

Bản đồ cần Internet và dùng public OpenStreetMap tiles; không còn cam kết chạy map hoàn toàn offline như bản cũ. Chỉ phục vụ prototype tương tác. Nền map thể hiện khu vực trung tâm, không tuyên bố bao trùm toàn bộ ranh giới hành chính TP.HCM.
