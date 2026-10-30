# Tài liệu yêu cầu nghiệp vụ — Cortex Sentinel MVP

Phiên bản: 1.0 · Ngày: 31/10/2026 (Asia/Ho_Chi_Minh)

Trạng thái: đề xuất đủ chi tiết để triển khai và trình các bên liên quan xem xét; không phải phê duyệt vận hành thực tế. Ngôn ngữ: tiếng Việt. Đơn vị phụ trách: nhóm sản phẩm; người bảo trợ nghiệp vụ và người phụ trách kỹ thuật cụ thể chưa được chỉ định. [Bản tiếng Anh](../BRD.md).

## 1. Quyết định tổng quan

Xây dựng một lớp điều tra tự chủ có giới hạn trên bộ máy xử lý giao dịch và tình huống nghiệp vụ hiện có, phục vụ chuyên viên rủi ro/gian lận ShopeePay cho cả ShopeePay và ShopeePayLater. Trình diễn bằng dữ liệu giả lập, bản đồ TP.HCM chi tiết, các khu vực cấu hình và hồ sơ riêng biệt, cùng khả năng thích nghi được đo lường và kiểm soát bằng phê duyệt.

Giả thuyết nghiệp vụ là việc thu thập bằng chứng và lặp lại các cuộc điều tra ít giá trị đang tiêu tốn sự chú ý của chuyên viên. Giả thuyết này chưa được xác nhận bằng phỏng vấn hoặc dữ liệu vận hành. Nghiên cứu công khai về Alipay/WeChat Pay ủng hộ kiểm soát nhiều lớp và quản trị, không chứng minh hiệu quả của chính giải pháp này.

MVP phải trình diễn hoạt động điều tra thực sự lúc chạy và kết quả đánh giá. Giao diện đẹp hoặc mức cải thiện được gán sẵn không đủ để tuyên bố hoàn thành mục tiêu của hạng mục Autonomous & Adaptive AI.

## 2. Hiện trạng và vấn đề

Theo thông tin người dùng, hệ thống đã có khả năng tiếp nhận dữ liệu và cấu hình tình huống nghiệp vụ. API, độ đầy đủ dữ liệu, thông lượng và khả năng tích hợp chưa được xác minh. Kho mã hiện có bản mẫu giao diện tương tác: bản đồ đường phố, bốn mục điều hướng, hồ sơ giả lập, kiểm tra cấu hình và phản hồi mô phỏng. Nó chưa có năng lực vận hành thực tế mà các màn hình thể hiện.

Chuyên viên cần hiểu những cảnh báo nào liên quan nhau, bằng chứng nào hỗ trợ hoặc phản bác nghi vấn, tác tử đã làm gì khi không có người giám sát và khi nào con người phải can thiệp. Không được đánh đổi chất lượng điều tra chỉ để giảm số cảnh báo.

## 3. Các bên liên quan và trách nhiệm

| Bên liên quan | Trách nhiệm / quyết định |
|---|---|
| Chuyên viên rủi ro | Kiểm tra hồ sơ, xác nhận tiếp nhận chuyển cấp, ghi kết luận dựa trên bằng chứng |
| Trưởng nhóm rủi ro | Sở hữu chính sách phân tuyến, phê duyệt cấu hình/điều chỉnh, cho phép hoàn tác |
| Người phụ trách sản phẩm | Phê duyệt phạm vi nghiệp vụ, tuyên bố trong trình diễn và bằng chứng nghiệm thu |
| Người phụ trách kỹ thuật | Xác minh hợp đồng tích hợp, triển khai độ tin cậy và ranh giới truy cập |
| Người rà soát đánh giá | Rà soát nhãn dữ liệu thử và trường hợp trọng yếu; đánh giá đầu ra độc lập với chỉ dẫn sinh kết quả |
| Ban giám khảo hackathon | Đánh giá giá trị được chứng minh, tính tự chủ, khả năng thích nghi và chất lượng xây dựng |

Một người có thể đảm nhiệm nhiều vai trò trong hackathon, nhưng việc đổi vai trò và sự kiện phê duyệt phải rõ ràng; không tuyên bố có phê duyệt độc lập nếu cùng một người thực hiện cả hai vai trò.

## 4. Mục tiêu nghiệp vụ và cách đo

| Mã | Mục tiêu | Đo lường và nghiệm thu MVP |
|---|---|---|
| BO-01 | Giảm thu thập bằng chứng lặp lại | So sánh luồng chỉ dùng quy tắc, bổ sung dữ liệu cố định và tác tử trên cùng bộ hồ sơ đã cố định; báo cáo thời gian xem xét gồm cả sửa lỗi |
| BO-02 | Điều tra tin cậy mà không cần giám sát liên tục | Năm lần chạy lại toàn trình đều hoàn tất hoặc chuyển rõ sang Cần xem xét; tình huống lỗi trọng yếu không biến mất hoặc bị coi là an toàn |
| BO-03 | Giữ lại tín hiệu gian lận quan trọng | Mọi mẫu gian lận trọng yếu được chỉ định đều được chuyển cấp; báo cáo gian lận bỏ sót và hồ sơ chưa xử lý trên toàn bộ mẫu có nhãn |
| BO-04 | Chứng minh khả năng thích nghi hữu ích | Một đề xuất có phạm vi làm giảm ít nhất một lần chuyển cấp nhầm trên tập đánh giá cố định mà không tăng gian lận bỏ sót; nếu không, báo cáo chưa có lợi ích được xác nhận và giữ phương án gốc |
| BO-05 | Cho phép kiểm tra lại quyết định | Mỗi nhận định có tham chiếu bằng chứng và điều chưa biết; mỗi kết luận/thay đổi chính sách có người thực hiện, thời gian và phiên bản |
| BO-06 | Hỗ trợ điều tra theo địa lý | Bản đồ đường phố TP.HCM và danh sách nhất quán; nguồn/độ bất định hiển thị rõ; hồ sơ thiếu vị trí vẫn truy cập được |

Đây là mục tiêu nghiệm thu hackathon được đề xuất, không phải kết quả quan sát, cam kết dịch vụ vận hành hay bảo đảm thống kê. Không tái sử dụng số minh họa 20→12 của giao diện như số đo. Nếu BO-04 không đạt, quy trình đánh giá có thể đã hoàn tất nhưng mục tiêu chứng minh lợi ích thích nghi vẫn chưa đạt.

## 5. Phạm vi nghiệp vụ

### Trong bản phát hành

- Tài khoản, đơn vị chấp nhận thanh toán, giao dịch, quan hệ thiết bị/mạng và hồ sơ lịch sử đã rà soát đều giả lập.
- Ba tình huống được tạo sẵn: phối hợp giữa các đơn vị chấp nhận thanh toán, bất thường vị trí, cụm thiết bị dùng chung; điều tra nhóm đơn vị phối hợp là tình huống chính, với cùng luồng công cụ tổng quát hỗ trợ các tình huống còn lại.
- Tái sử dụng bộ máy hiện có qua bộ chuyển đổi đã xác minh; nếu không truy cập được, dùng bộ chuyển đổi giả lập có ghi nhãn rõ.
- Điều tra bất đồng bộ, truy vấn quan hệ, kiểm tra phản chứng, phục hồi có giới hạn, tạo hồ sơ hợp nhất và chuyển cấp nội bộ.
- Bốn mục: Bản đồ, Cấu hình, Hồ sơ rủi ro, Nhật ký hoạt động.
- Kết luận chuyên viên, đề xuất điều chỉnh có phạm vi, đánh giá chạy lại thực sự, phê duyệt rõ ràng, quản lý phiên bản và hoàn tác.
- Bản trình diễn có thể tái lập, kết quả đánh giá được đo và công bố trung thực giới hạn.

### Ngoài phạm vi

Dữ liệu khách hàng thật; thực thi thanh toán thật; tự động từ chối thanh toán, khóa tài khoản hoặc quyết định tín dụng; gửi báo cáo chống rửa tiền cho cơ quan quản lý; chương trình sàng lọc cấm vận; tuân thủ chống rửa tiền toàn diện; xác nhận ranh giới hành chính toàn thành phố; mạng nơ-ron đồ thị đã huấn luyện; nền tảng kho đặc trưng luồng dữ liệu mới; huấn luyện lại trực tuyến liên tục; gửi thư điện tử/SMS bên ngoài; điều hướng bản đồ toàn cầu; đường nối quan hệ trên bản đồ.

## 6. Quy tắc nghiệp vụ

1. Cảnh báo, nhận định đáng ngờ, kết luận xác nhận gian lận và phát hiện rửa tiền là các khái niệm khác nhau. MVP không xác định tội danh pháp lý.
2. Thiếu bằng chứng phải được chuyển để xem xét. Ưu tiên thấp không đồng nghĩa tự động xác nhận an toàn hoặc đóng hồ sơ.
3. Mô hình được điều tra và đề xuất; chính sách xác định quyết định tuyến được phép. Chỉ người có quyền mới được kích hoạt thay đổi chính sách.
4. IP dùng chung, khoảng cách địa lý hoặc nợ quá hạn riêng lẻ không đủ xác lập gian lận. Khoản vay được phép không phải rút tiền qua giao dịch giả.
5. TP.HCM là phạm vi bản đồ/trình diễn, không phải giới hạn bằng chứng: hoạt động liên quan ngoài khu vực vẫn xuất hiện trong bằng chứng hồ sơ.
6. Bộ lọc hiển thị bản đồ không sửa quy tắc phát hiện. Việc ẩn/lọc ở trình duyệt không thay đổi phân quyền phía máy chủ.
7. Phản hồi chuyên viên là quan sát được rà soát, không phải sự thật không thể sai. Chỉ quyết định đã xác thực mới thành ngữ cảnh truy xuất; nhãn đánh giá được giữ riêng.
8. Không đưa bí mật ứng dụng hoặc dữ liệu tài khoản nhạy cảm vào URL nhà cung cấp bản đồ hay lệnh gọi mô hình từ trình duyệt.

## 7. Hành trình nghiệp vụ

Chọn cấu hình giám sát hiện có → xem bản đồ TP.HCM hoặc danh sách hồ sơ → tác tử thu thập bằng chứng bất đồng bộ → chính sách phân tuyến hồ sơ hợp nhất → chuyên viên xác nhận tiếp nhận/xem xét → lưu kết luận có lý do → đánh giá đề xuất điều chỉnh → trưởng nhóm phê duyệt hoặc từ chối → kích hoạt phiên bản hoặc giữ bản gốc → có thể hoàn tác.

Chỉnh cấu hình là hành trình riêng, không bắt buộc: chọn cấu hình → sửa bản nháp → chạy lại kiểm tra → xem kết quả → phê duyệt/áp dụng → giám sát. Không có trình thiết lập bắt buộc trước khi xem dữ liệu tạo sẵn.

## 8. Cơ sở nghiên cứu

[Nghiên cứu Alipay](../../research/alipay-wechat-bnpl/alipay-findings.md) ghi nhận kiểm soát đơn vị chấp nhận thanh toán/danh tính và tuyên bố chống rửa tiền cấp tập đoàn cùng giới hạn nguồn. [Nghiên cứu WeChat](../../research/alipay-wechat-bnpl/wechat-findings.md) ghi nhận đánh giá giao dịch thời gian thực, mục đích xử lý dữ liệu thiết bị/mạng và quản trị. Không tài liệu nào chứng minh mô hình đồ thị, tính tự chủ của mô hình ngôn ngữ lớn hoặc mức giảm cảnh báo nhầm của sản phẩm này. Bối cảnh hợp đồng/quy định Trung Quốc không được coi là kết luận tuân thủ tại Việt Nam.

[Báo cáo khả thi](../Solution-feasibility-report.md) ủng hộ tiếp tục xây một luồng xuyên suốt trong môi trường thử nghiệm có giám sát. Bản đồ giúp định hướng; phân loại và điều phối xử lý dựa trên bằng chứng mới là năng lực khác biệt.

## 9. Giả định, phụ thuộc và rủi ro

| Hạng mục | Giả định làm việc / cách xử lý | Phụ trách |
|---|---|---|
| Truy cập bộ máy hiện có | Xác minh lược đồ và bộ chuyển đổi trước triển khai; công bố phương án giả lập thay thế | Kỹ thuật |
| Nhân lực/thời gian | Chưa rõ; ưu tiên P0 trong PRD, bỏ P1/P2 trước khi giảm tiêu chí bằng chứng | Sản phẩm |
| Tiếp cận chuyên viên | Tìm 2–3 chuyên viên; ghi rõ người cùng nhóm là người dùng thay thế nếu cần | Sản phẩm |
| Khả dụng mô hình | Có thông tin xác thực phía máy chủ và ngân sách; quá hạn phải chuyển xem xét rõ ràng | Kỹ thuật |
| Nhãn dữ liệu | Rà soát nhãn giả lập trước đánh giá; ngăn rò rỉ theo nhóm liên quan/thời gian | Đánh giá |
| Nhà cung cấp bản đồ | Có ràng buộc mạng/điều khoản; lỗi map không chặn luồng danh sách | Kỹ thuật |
| Phản hồi sai hoặc bị thao túng | Đề xuất giới hạn phạm vi, rà soát, tập kiểm tra giữ riêng, nhật ký và hoàn tác | Trưởng nhóm rủi ro |
| Tuyên bố quá mức | Tách phần đã triển khai, giả lập, đo được và dự kiến | Sản phẩm |

## 10. Nghiệm thu nghiệp vụ và bàn giao

Phát hành cần đạt toàn bộ tiêu chí P0 trong PRD, có kết quả phương án gốc/đề xuất được ghi lại, xử lý lỗi trọng yếu, một quy trình đặt lại/chạy có thể tái lập và bằng chứng/nhật ký kiểm tra được. Không tuyên bố cải thiện đã được phê duyệt nếu đánh giá thích nghi thất bại. Trình diễn vẫn phải cho phép từ chối đề xuất không cải thiện.

Bàn giao gồm mã lần lưu Git, danh mục mẫu thử, phiên bản cấu hình/mô hình/chỉ dẫn, báo cáo đánh giá có số đếm và thời gian gốc, giới hạn đã biết và kịch bản trình diễn sáu phút. Phê duyệt nghiệp vụ không cho phép thực hiện hành động tài chính thật.

## 11. Sau hackathon

Thí điểm cần phỏng vấn chuyên viên thật, rà soát quyền truy cập/pháp lý, nhãn xác thực, kiểm soát truy cập được lưu bền vững và giám sát vận hành. Xác định nghiên cứu chế độ chạy song song quan sát có thời hạn trước khi can thiệp giao dịch thật. Chỉ dự báo tiết kiệm công sức từ thay đổi thời gian tác vụ đã đo và tần suất thực tế; hiện chưa có cơ sở tuyên bố hiệu quả đầu tư hoặc ngăn tổn thất.
