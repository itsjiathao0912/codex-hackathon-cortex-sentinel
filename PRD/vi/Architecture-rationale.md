# Cơ sở lựa chọn kiến trúc — quyết định triển khai MVP

Ngày: 31/10/2026. [Bản tiếng Anh](../Architecture-rationale.md). Tài liệu đi kèm [thiết kế triển khai](../Implementation-design.md). [PRD](PRD.md) quy định hành vi mục tiêu hiện hành; tài liệu này giải thích vì sao các lựa chọn phù hợp MVP. Thiết kế kỹ thuật tiếng Việt trước đây là tài liệu nền, không phải bằng chứng đã triển khai.

## Hiện trạng so với mục tiêu

| Năng lực | Hiện vật hiện có trong kho mã | Phần cần triển khai |
|---|---|---|
| Bản đồ TP.HCM và bốn mục | Bản mẫu HTML hoạt động, Leaflet và ảnh ô bản đồ trực tuyến | Hồ sơ qua API, phân quyền, cập nhật ổn định |
| Kiểm tra/áp dụng cấu hình | Kết quả minh họa cố định, phiên bản trong bộ nhớ | Kiểm tra dựa trên dữ liệu, mã băm, kiểm tra vai trò, phiên bản bền vững |
| Điều tra AI | Chưa triển khai trong bản mẫu | Tiến trình xử lý phía máy chủ, công cụ chỉ đọc, kiểm tra đầu ra mô hình |
| Chuyển cấp | Văn bản/trạng thái giả lập | Hàng đợi gửi bền vững, chuyển giao nội bộ, xác nhận tiếp nhận và tuyến dự phòng |
| Phản hồi/thích nghi | So sánh theo kịch bản và trạng thái giao diện | Ngữ cảnh đã rà soát, đánh giá thật trên tập giữ riêng, phê duyệt và hoàn tác |
| Nhật ký kiểm toán | Sự kiện trong bộ nhớ | Sự kiện ứng dụng bền vững chỉ ghi nối tiếp, kèm người thực hiện và phiên bản |

## Ghi nhận quyết định

| Quyết định | Lý do | Phương án hoãn / đánh đổi | Cách xác minh |
|---|---|---|---|
| Tái sử dụng bộ phát hiện, điều tra bất đồng bộ | Không đưa độ trễ/lỗi mô hình vào đường cấp phép thanh toán; tận dụng đầu tư hiện có theo thông tin người dùng | Chấm điểm bằng mô hình ngay trên đường thanh toán có thể tạo nút thắt; bất đồng bộ không ngăn được thanh toán đã hoàn thành | Đo thời gian chờ và điều tra; công bố không chặn thanh toán |
| Một tác tử với công cụ chỉ đọc có giới hạn | Thể hiện tự chọn bước tiếp theo với bề mặt quyền hạn nhỏ, dễ kiểm tra | Điều phối nhiều tác tử tăng chi phí phối hợp trước khi chứng minh lợi ích | So sánh với bổ sung dữ liệu cố định, kiểm tra lựa chọn công cụ |
| Quy tắc quyết định tuyến, mô hình đề xuất nhận định | Tách phán đoán có tính xác suất khỏi quyền thực thi; bảo toàn tín hiệu rủi ro cao | Mô hình phân tuyến trực tiếp đơn giản hơn nhưng khó giới hạn/kiểm toán | Từ chối đầu ra sai, kiểm tra giữ tín hiệu trọng yếu |
| Truy vấn quan hệ trước mạng nơ-ron đồ thị | Dữ liệu mẫu nhỏ không cần huấn luyện hoặc hạ tầng đồ thị mới | Mô hình đồ thị có thể hữu ích sau này nhưng cần nhãn, huấn luyện và so sánh | Loại bỏ bước mở rộng quan hệ để so sánh với phương án gốc |
| Tiền lệ đã rà soát và điều chỉnh chính sách có phạm vi | Chứng minh học từ phản hồi mà không huấn luyện lại; giải thích và hoàn tác được | Tinh chỉnh/huấn luyện trực tuyến cần nhiều dữ liệu và kiểm soát nhãn hơn | Cải thiện trên tập giữ riêng kèm ràng buộc gian lận bỏ sót |
| Công việc trong cơ sở dữ liệu và hàng đợi gửi bền vững | Kiến trúc nhỏ, dễ triển khai, liên kết hồ sơ và gửi thông báo trong giao dịch dữ liệu | Hệ thống trung gian hàng đợi riêng hữu ích khi lớn nhưng chưa cần cho môi trường thử nhỏ | Kiểm tra sập tiến trình, thử lại và gửi trùng |
| Bản đồ đường phố TP.HCM bằng Leaflet | Đã triển khai, hỗ trợ chi tiết và màu trung tính ấm; không cần bản đồ thế giới/đường nối | Nền tảng 3D/vector tăng phạm vi; ảnh bản đồ phụ thuộc mạng/nhà cung cấp | Kiểm tra nguồn vị trí, bàn phím/danh sách dự phòng, lỗi tải map |
| Tách cấu hình/hồ sơ/nhật ký | Đúng yêu cầu sửa của người dùng, tránh quá tải map | Một màn hình giảm điều hướng nhưng thiết kế trước quá nhiều nội dung | Quan sát chuyên viên hoàn thành tác vụ map và cấu hình |
| Hỏi dữ liệu định kỳ trước SSE | Cập nhật/phục hồi đơn giản cho lưu lượng demo vừa phải | SSE giảm chi phí hỏi định kỳ nhưng thêm xử lý nối lại/trạng thái | Giữ lựa chọn/khung map ổn định, giới hạn lỗi cập nhật |
| Ba máy trạng thái vận hành độc lập | Hoàn tất điều tra, kết luận hồ sơ và chuyển giao cảnh báo là những sự kiện khác nhau | Một trường trạng thái tạo nhập nhằng như đã gửi = đã giải quyết | Mẫu chuyển trạng thái và kiểm tra nhật ký |

## Đường đi dữ liệu khi chạy

Trình duyệt → API ứng dụng có xác thực → cơ sở dữ liệu và hàng đợi công việc → tiến trình xử lý → công cụ bằng chứng trong danh sách cho phép → mô hình bên ngoài → bộ kiểm tra đầu ra → bộ phân tuyến theo quy tắc xác định → hồ sơ và hàng đợi gửi → giao diện chuyên viên.

Trong MVP chỉ có bằng chứng giả lập được tối thiểu hóa rời ứng dụng. Thông tin xác thực API ở phía máy chủ. Văn bản giao dịch là dữ liệu công cụ không đáng tin. Mô hình không có kết nối cơ sở dữ liệu tùy ý, thông tin xác thực, công cụ truy cập URL không giới hạn hoặc khả năng tác động tài khoản.

Ảnh ô bản đồ đi theo đường riêng từ trình duyệt đến nhà cung cấp, chứa yêu cầu vùng nhìn chứ không chứa mã hồ sơ. Giữ ghi công nguồn và yêu cầu bộ nhớ đệm/thông tin trang giới thiệu; dùng ảnh phản hồi giả lập khi kiểm thử tự động. Cần rà soát khả dụng và điều khoản cho triển khai thật; không suy ra cam kết dịch vụ từ truy cập OSM công cộng.

## Đồng bộ với thiết kế trước

Giới hạn 8 lần gọi trong PRD tính cả thử lại. Hạn 30 giây gồm các lần thử lại công cụ nhưng không gồm thời gian chờ hàng đợi. Mặc định PRD thay thế giả định minh họa 3 phút/12 lần gọi trước đây. Trạng thái hồ sơ, điều tra và chuyển giao tách riêng, thay cho mô tả vòng đời gộp trước đây.

Map chỉ hiển thị TP.HCM trong khi truy xuất bằng chứng có phân quyền vẫn có thể bao gồm hoạt động liên quan ngoài khu vực. Hộp giới hạn tọa độ là ràng buộc hiển thị, không phải đa giác hành chính đã xác minh hoặc quy tắc loại bằng chứng. Không tạo điểm map giả khi không biết vị trí.

## Điều gì có thể làm thay đổi lựa chọn?

- Áp lực thông lượng/hàng đợi đã đo có thể là cơ sở thêm hệ thống trung gian hoặc dịch vụ đặc trưng luồng dữ liệu.
- Mạng nơ-ron đồ thị đã huấn luyện phải vượt phương án gốc công bằng trên các nhóm giữ riêng được gán nhãn độc lập trước khi trở thành phụ thuộc.
- Tải hoặc độ trễ hỏi dữ liệu định kỳ đã đo có thể là lý do dùng SSE.
- Độ mơ hồ địa lý hoặc giới hạn nhà cung cấp đã chứng minh có thể là lý do dùng ô bản đồ vector, gom cụm hoặc nhà cung cấp có hợp đồng/riêng.
- Vận hành thật cần rà soát sẵn sàng riêng; hoàn thành demo hackathon không cho phép can thiệp tài chính thật.
