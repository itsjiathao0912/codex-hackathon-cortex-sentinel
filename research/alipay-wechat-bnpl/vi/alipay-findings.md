# Alipay / Ant / Huabei: bằng chứng về gian lận và phòng, chống rửa tiền

[Bản gốc tiếng Anh](../alipay-findings.md)

Ngày nghiên cứu: 31 tháng 10 năm 2026. Phạm vi: Trung Quốc đại lục. Đây là nghiên cứu từ các nguồn công khai, không phải mô tả các ngưỡng phát hiện chưa công khai hoặc cuộc kiểm toán về hiệu quả vận hành. Các phần tóm lược nguồn tiếng Trung dưới đây được chuyển ngữ từ bản diễn giải bằng tiếng Anh.

## Phân định sản phẩm và pháp nhân

**A1 — Phạm vi sản phẩm hiện tại (độ tin cậy cao).** Bản công bố sản phẩm của Ant Consumer Finance, đề ngày **31 tháng 7 năm 2026**, mô tả Huabei là tín dụng tiêu dùng quay vòng không có tài sản bảo đảm, với các tính năng mua hàng/trả góp. Tài liệu cũng nêu rõ **các khoản vay tiêu dùng Huabei dạng tiền mặt**. Vì vậy, cần phân biệt mua trước trả sau (BNPL) để mua hàng với vay tiền mặt được phép và hành vi bị cấm là rút tiền thông qua giao dịch giả tạo. Không nên lặp lại những khẳng định tuyệt đối trước đây rằng Huabei không bao giờ có thể giải ngân tiền mặt. Bản công bố này nằm trên trang web doanh nghiệp của Ant Consumer Finance, chứ không đơn thuần là trang tiếp thị ví Alipay. [S1]

Đơn vị vận hành ví/thanh toán và bên cung cấp dịch vụ tín dụng có vai trò riêng biệt. Hợp đồng Huabei chính thức có thể truy cập công khai mô tả Alipay (China) Network Technology Co., Ltd. là bên phụ trách tài khoản thanh toán/định tuyến thanh toán, đồng thời đề cập riêng đến các bên cung cấp dịch vụ tín dụng. Tuy nhiên, nội dung về nhiều bên cung cấp, bao thanh toán và cho vay nhỏ lẻ **không ghi ngày và có thể thuộc phiên bản cũ**; không được xem đây là danh sách đầy đủ các bên cho vay vào tháng 10 năm 2026. Cần có thỏa thuận hiện hành trong ứng dụng của khách hàng để xác định chính xác bên cho vay và các điều khoản áp dụng. [S2]

## Những điều được bằng chứng công khai hỗ trợ

| Nhận định | Biện pháp kiểm soát và bằng chứng | Phạm vi / độ tin cậy |
|---|---|---|
| A2 | Hợp đồng Huabei được công bố quy định việc xác minh danh tính, yêu cầu cung cấp thông tin chính xác, đánh giá rủi ro và thay đổi hạn mức tín dụng. Các phần liên quan: Điều IV, VI và VII. | Các cơ chế hợp đồng riêng của Huabei; độ tin cậy cao đối với nội dung văn bản, chưa xác nhận khả năng áp dụng của phiên bản hiện hành. Việc thay đổi hạn mức kết hợp cả rủi ro tín dụng và rủi ro giao dịch; không mặc nhiên là quyết định về phòng, chống rửa tiền (AML). [S2] |
| A3 | Hợp đồng cấm rút tiền thông qua giao dịch giả tạo và tạo đơn hàng giả; cho phép tạm dừng giao dịch vì lo ngại về an toàn; quy định quyền tiếp cận thông tin giao dịch/hoàn tiền/tranh chấp; và nêu rằng thông tin có thể được sử dụng để chống rửa tiền và rút tiền thông qua giao dịch giả tạo. Điều IV.4, V.1, VI.1.4 và VII.2.5. | Các quyền theo hợp đồng dành riêng cho sản phẩm; không phải bằng chứng về mô hình cụ thể đã triển khai, tỷ lệ phát hiện hoặc quy trình nộp báo cáo giao dịch đáng ngờ. [S2] |
| A4 | Thỏa thuận dành cho đơn vị chấp nhận thanh toán của Alipay yêu cầu thông tin danh tính, hoạt động kinh doanh/giấy phép và dữ liệu giao dịch của đơn vị; các đối tác tham gia phải hỗ trợ xác minh khách hàng, thông báo giao dịch có rủi ro và phản hồi thông tin rủi ro. | Các biện pháp kiểm soát ở lớp đơn vị chấp nhận thanh toán/thanh toán, **không chỉ riêng Huabei**. Thỏa thuận công khai không ghi ngày. [S3] |
| A5 | Thỏa thuận đó cho phép điều tra, tạm dừng/chấm dứt kênh thanh toán, giới hạn thanh toán/nhận tiền và trì hoãn quyết toán khi nghi ngờ có gian lận, rút tiền thông qua giao dịch giả tạo, rửa tiền hoặc tài trợ khủng bố; đồng thời cho phép báo cáo nghi vấn tội phạm viễn thông/mạng cho cảnh sát. | Các quyền thực thi hợp đồng thanh toán được ghi nhận bằng văn bản. Báo cáo cho cảnh sát **không đồng nghĩa với báo cáo giao dịch đáng ngờ theo cơ chế AML**. Các điều khoản áp dụng bao gồm 3.2.5–3.2.6. [S3] |
| A6 | Đơn vị chấp nhận thanh toán không được lưu giữ thông tin xác thực thanh toán nhạy cảm; việc chia sẻ thông tin và truy cập phải tuân thủ các quy định về an toàn/bảo mật. | Bảo vệ dữ liệu trong hệ sinh thái thanh toán; không phải bản thống kê đầy đủ về quyền riêng tư của Huabei hay bằng chứng rằng mọi kho dữ liệu ở các hệ thống liên quan đều tuân thủ. [S3] |
| A7 | Thông cáo do công ty phát hành vào tháng 7 năm 2025 mô tả khung AML thống nhất của Ant, các chỉ báo được chuẩn hóa, RiskKey/iGuardian và việc tự động hóa báo cáo giao dịch đáng ngờ. Thông cáo đề cập AI, xử lý hình ảnh bằng máy tính và các mô hình ngôn ngữ lớn (LLM). | **Thông tin do Ant tự công bố ở cấp toàn tập đoàn**, bao trùm hoạt động toàn cầu; không có bằng chứng cho thấy mọi năng lực được nêu đều được triển khai trong Huabei hoặc LLM tự quyết định có nộp báo cáo hay không. Không được mô tả các tuyên bố của nhà cung cấp như kết quả đã được kiểm toán độc lập. [S4] |
| A8 | Bài viết của Tân Hoa Xã vào tháng 6 năm 2026 về báo cáo phát triển bền vững năm 2025 của Ant Consumer Finance mô tả việc đánh giá theo từng bối cảnh sử dụng trong thời gian thực dựa trên danh tính, loại đơn vị chấp nhận thanh toán, danh mục sản phẩm và giá, cùng với việc ra quyết định linh hoạt và nhận diện gian lận. | Thông tin gần đây dành riêng cho bên cho vay, nhưng là **bài viết thứ cấp về báo cáo của công ty**, không phải chính báo cáo đó. Bài viết không công bố trọng số đặc trưng, tỷ lệ nhận diện nhầm giao dịch hợp lệ là gian lận hay quy trình AML. [S5] |

## Diễn giải theo vòng đời

1. **Tiếp nhận khách hàng / tính toàn vẹn của tài khoản:** xác lập danh tính và tính trung thực của thông tin đăng ký. Hợp đồng Huabei quy định rõ việc bảo vệ tài khoản/mật khẩu/mã xác minh và báo cáo hành vi mạo danh. Các tài liệu riêng về BNPL đã truy xuất chưa xác lập được cách triển khai cụ thể hiện nay của sinh trắc học và kỹ thuật tạo dấu vân tay thiết bị. [S2]
2. **Quyết định tín dụng:** đánh giá khả năng và thiện chí trả nợ, thiết lập và điều chỉnh hạn mức. Đây chủ yếu là rủi ro tín dụng. Quyết định này có thể sử dụng bằng chứng trùng với mô hình phát hiện gian lận nhưng vẫn là một loại quyết định riêng. [S2]
3. **Kiểm soát mua hàng / đơn vị chấp nhận thanh toán:** kết hợp quyết định cho vay với lớp thanh toán/đơn vị chấp nhận thanh toán có khả năng xác minh đơn vị, tiếp nhận tín hiệu rủi ro và ngắt giao dịch đáng ngờ. Cách kết hợp cụ thể này là diễn giải về kiến trúc từ S2/S3, không phải sơ đồ triển khai đã được công bố.
4. **Sau mua hàng:** quyền theo hợp đồng được tiếp cận thông tin hoàn tiền/tranh chấp và quản lý nguồn tiền trả nợ hỗ trợ giám sát liên tục. Thu hồi nợ và báo cáo thông tin tín dụng liên quan đến tình trạng thực hiện nghĩa vụ trả nợ; bản thân mỗi hoạt động đều không chứng minh có rửa tiền. [S2]
5. **Hoạt động AML:** Ant mô tả việc quản trị chỉ báo và tự động hóa báo cáo ở cấp tập đoàn. Bằng chứng công khai chưa xác lập được hàng đợi rà soát cảnh báo riêng của Huabei, các bước phê duyệt của điều tra viên, nhà cung cấp danh sách sàng lọc, ngưỡng, số lượng báo cáo hoặc chỉ số dương tính giả/âm tính giả. [S4]

## Không nên đánh đồng gian lận, AML và rút tiền thông qua giao dịch giả tạo

- Lạm dụng danh tính hoặc chiếm đoạt tài khoản liên quan đến việc người vay/hành động thanh toán có xác thực hay không.
- Giao dịch mua bán giả tạo nhằm chuyển tín dụng mua hàng thành tiền mặt bị cấm rõ ràng trong hợp đồng sản phẩm đã công bố; đây là vấn đề về gian lận/sử dụng sản phẩm theo hợp đồng và cũng có thể là tín hiệu tội phạm tài chính.
- Tính năng vay tiền mặt được phép trong bản công bố sản phẩm hiện hành **không** đồng nghĩa với hành vi bị cấm đó.
- Rửa tiền liên quan đến tiền, tài sản có nguồn gốc bất hợp pháp và việc che giấu/di chuyển chúng. Cảnh báo rủi ro, giao dịch thanh toán bị từ chối, báo cáo giao dịch đáng ngờ và hành vi phạm tội đã được chứng minh là những trạng thái khác nhau.
- Nợ quá hạn, khả năng chi trả, thu hồi nợ và trích lập dự phòng tổn thất cho vay là các vấn đề về rủi ro tín dụng, trừ khi có thêm bằng chứng hỗ trợ cách diễn giải theo hướng gian lận/AML.

## Danh mục nguồn và hạn chế

Tất cả các nguồn được truy cập vào ngày 31 tháng 10 năm 2026.

| ID | Nguồn / ngày | Loại nguồn và cách sử dụng |
|---|---|---|
| S1 | [Bản công bố sản phẩm của Ant Consumer Finance](https://www.myxiaojin.cn/notice/detail/6), nội dung ghi ngày 2026-07-31 | Bản công bố sản phẩm hiện hành từ nguồn sơ cấp; đã truy xuất toàn văn. Có nội dung về sản phẩm Huabei dạng tiền mặt. |
| S2 | [Hợp đồng Huabei được công bố](https://render.alipay.com/p/f/platform/index.html?bizScenario=ch_alipay_chs), không hiển thị ngày có hiệu lực | Văn bản hợp đồng sơ cấp trên tên miền chính thức; đã truy xuất toàn văn, nhưng chưa chắc chắn về phiên bản/bên cho vay áp dụng và có nội dung thuộc dạng cũ. Chỉ sử dụng để xác định các biện pháp kiểm soát theo hợp đồng đã công bố. |
| S3 | [Hợp đồng dịch vụ sản phẩm Alipay dành cho đơn vị chấp nhận thanh toán](https://render.alipay.com/p/f/fd-jqw79r4v/index.html), không hiển thị ngày có hiệu lực | Thỏa thuận thanh toán/đơn vị chấp nhận thanh toán sơ cấp trên tên miền chính thức; đã truy xuất toàn văn. Không dành riêng cho Huabei. |
| S4 | [Thông báo về AML/GRC do Ant phát hành, được Medianet đăng lại](https://newshub.medianet.com.au/2025/07/ant-group-recognized-for-best-aml-technology-initiative-in-asia-pacific-and-best-grc-implementation-in-china/109098/), 2025-07-10 | Thông cáo báo chí sơ cấp của công ty, ghi rõ Ant là đơn vị phát hành và có liên kết nguồn Business Wire; đã truy xuất toàn văn. Thông tin tự công bố ở cấp tập đoàn. URL Business Wire gốc bị cơ chế chống bot chặn. |
| S5 | [Bài viết của Tân Hoa Xã về báo cáo phát triển bền vững năm 2025 của Ant Consumer Finance](http://www.news.cn/tech/20260629/d085a90894974211953f92252c88bf81/c.html), URL/nội dung cho thấy ngày 2026-06-29 | Bài viết thứ cấp về báo cáo của công ty; đã truy xuất toàn văn. Cung cấp bối cảnh gần đây hữu ích về bên cho vay, không phải bằng chứng độc lập về hiệu quả. |

**Các lần truy cập không thành công:** TinyFish trả về nội dung trống đối với trang ESG doanh nghiệp của Ant, trang thông cáo báo chí về báo cáo năm 2024, trang chủ Ant Consumer Finance và các trang về quyền riêng tư của Alipay SDK; Business Wire bị cơ chế chống bot chặn. Các đoạn trích kết quả tìm kiếm về dữ liệu thiết bị/danh tính của SDK **không được nâng thành nhận định đã xác minh**. HTML của trang chủ cũng được truy xuất trực tiếp nhưng không hiển thị nội dung doanh nghiệp có ý nghĩa, nên không cung cấp thêm bằng chứng. Không truy cập tài liệu mật nào.

**Số lượng:** sử dụng năm nguồn toàn văn riêng biệt (bốn tài liệu nguồn sơ cấp, trong đó có một thông cáo của đơn vị phát hành được đăng lại, và một bài viết thứ cấp). Một số kết quả tìm kiếm bổ sung và các lần truy xuất thất bại chỉ được xem xét như đầu mối tìm nguồn; không có tổng số “nguồn đã rà soát” nào tính chúng là tài liệu đã đọc toàn văn. Các kết quả về hợp đồng Huabei cũ và bình luận không chính thức đã bị loại khỏi tập bằng chứng về thực tiễn hiện hành.

**Các nội dung cần xác minh tiếp theo với mức ưu tiên cao nhất:** thu thập thỏa thuận cho vay/thông báo quyền riêng tư Huabei hiện hành trong ứng dụng cho đúng sản phẩm và bên cho vay; thu thập báo cáo phát triển bền vững năm 2025 bản gốc của Ant Consumer Finance; thu thập mọi công bố riêng của sản phẩm về quản trị AML, rà soát của con người và lưu giữ dữ liệu cá nhân. Khi chưa có các tài liệu đó, các phát hiện trên cần giữ nguyên phạm vi và mức độ chưa chắc chắn đã nêu.
