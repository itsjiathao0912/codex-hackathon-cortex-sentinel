# WeChat Pay / Fenfu: bằng chứng về gian lận và phòng, chống rửa tiền

[Bản gốc tiếng Anh](../wechat-findings.md)

Ngày nghiên cứu: 31 tháng 10 năm 2026. Phạm vi: Trung Quốc đại lục, các nguồn công khai. Các nguồn xác lập cách thức vận hành sản phẩm được công bố, quyền theo hợp đồng và chính sách cấp tập đoàn; chúng không xác minh độc lập hiệu quả hoặc tiết lộ các ngưỡng quy tắc nội bộ. Chín trang/PDF nguồn sơ cấp riêng biệt đã được truy xuất bằng TinyFish, không có lỗi truy xuất. Các đoạn trích trong kết quả tìm kiếm chỉ được dùng để tìm nguồn.

## Phân biệt các chủ thể và sản phẩm

Fenfu (分付) là sản phẩm tín dụng tiêu dùng tích hợp trong WeChat; sản phẩm này không đồng nhất với dịch vụ thanh toán hay WeChat Pay Score. Cơ chế dư nợ quay vòng tính lãi theo ngày mặc định của Fenfu không tương đương với một sản phẩm “trả làm bốn kỳ” miễn lãi áp dụng phổ biến. Hướng dẫn tháng 6 năm 2026 cũng mô tả hình thức trả góp miễn lãi tại một số thương nhân đối tác, tính năng chuyển tiền đang dần được mở và tính năng vay tiền về tài khoản ngân hàng đang được thử nghiệm. Khả năng sử dụng phụ thuộc vào tài khoản và các điều khoản sản phẩm được hiển thị. [W1]

Một hợp đồng của JinCheng Consumer Finance nêu rõ công ty này là bên cho vay, Tenpay Payment Technology (财付通支付科技有限公司) là đơn vị vận hành thanh toán và Chongqing Weiheng Technology (重庆市微恒科技有限公司) là đơn vị tư vấn công nghệ/dịch vụ. Hợp đồng mô tả tín dụng mua hàng được giải ngân cho đối tác giao dịch và tín dụng sau tiêu dùng được giải ngân vào tài khoản ngân hàng đứng tên chính người vay. Đây là hợp đồng của một đối tác, không phải bằng chứng rằng JinCheng cấp vốn cho mọi khoản vay Fenfu. [W2]

Một công bố riêng của DBS China đề ngày 9 tháng 9 năm 2026 mô tả việc hợp tác Fenfu với Shenzhen Tenpay Network Finance Microloan (深圳市财付通网络金融小额贷款有限公司) và Weiheng. Công bố quy định tỷ lệ cấp vốn cho thỏa thuận đó là 70% DBS / 30% Tenpay Microloan. Độ tuổi của người đăng ký theo thỏa thuận này là từ 23 tuổi, trong khi hướng dẫn sản phẩm chung nêu từ 18 tuổi: cần phân biệt điều kiện của đối tác với điều kiện của nền tảng, thay vì coi đây là một quy tắc chung duy nhất. [W3]

WeChat Pay Score (微信支付分) đánh giá thông tin trong hệ sinh thái thanh toán và hỗ trợ thương nhân quyết định có cung cấp các tiện ích như miễn đặt cọc và dùng trước, trả sau hay không. Thỏa thuận tháng 8 năm 2026 quy định điểm này không được sử dụng cho các dịch vụ tài chính về cấp vốn/tín dụng. Không được tự động coi các trường dữ liệu của điểm số là đầu vào đã được chứng minh cho việc thẩm định tín dụng Fenfu. [W4]

Hướng dẫn Fenfu phân biệt rõ Fenfu với Weilidai (微粒贷). Danh mục của DBS liệt kê riêng một hợp tác Weilidai với WeBank. Không gọi Fenfu là “BNPL (mua trước, trả sau) của WeBank” hoặc đánh đồng hai sản phẩm. [W1, W9]

## Các biện pháp kiểm soát riêng của sản phẩm được ghi nhận

| Nhận định | Cách thức vận hành được ghi nhận công khai | Nhóm rủi ro | Bằng chứng và mức độ tin cậy |
|---|---|---|---|
| W-C1 | Điều kiện sử dụng yêu cầu danh tính thật của người trưởng thành, thẻ ngân hàng tại Trung Quốc đại lục, trạng thái tài khoản thanh toán bình thường và mỗi danh tính chỉ có một tài khoản Fenfu. | Tính toàn vẹn của danh tính/tài khoản; điều kiện cấp tín dụng | W1 §§2.2–2.3. Cao đối với các điều kiện được công bố, không phải hiệu quả. |
| W-C2 | Giao dịch được hệ thống đánh giá theo thời gian thực; các giao dịch rủi ro và một số mục đích sử dụng bị hạn chế. Hướng dẫn nêu rằng bộ phận chăm sóc khách hàng không thể thay đổi kết quả đánh giá đó. | Gian lận/rủi ro giao dịch | W1 §§2.4, 3.3, 3.6. Cao; không công bố đặc trưng đầu vào hoặc ngưỡng. |
| W-C3 | Việc cập nhật giấy tờ định danh được liên hệ rõ ràng với luật phòng, chống rửa tiền (AML) và hướng dẫn về AML/chống tài trợ khủng bố (CFT) dành cho bên cho vay nhỏ trực tuyến. Không cập nhật sẽ bị hạn chế sử dụng. | Nhận biết khách hàng (KYC)/AML liên tục | W1 §3.7. Cao, có liên hệ AML trực tiếp và riêng cho sản phẩm. |
| W-C4 | Các hạn chế về mục đích vay cấm rút tiền mặt trái phép thông qua giao dịch, tạo đơn hàng giả và rửa tiền. Hành vi rủi ro có thể dẫn đến đình chỉ giao dịch hoặc hạn chế dịch vụ. | Gian lận, mục đích sử dụng bị cấm, kiểm soát liên quan đến AML | W2 Điều 3–4. Cao đối với hợp đồng của bên cho vay này. |
| W-C5 | Hợp đồng cho phép thu thập dữ liệu danh tính/xác minh, mục đích vay, giao dịch, luồng giải ngân/trả nợ và thiết bị/mạng/nhật ký để thực hiện trách nhiệm AML và chống lừa đảo; thông tin rủi ro tài khoản từ đối tác có thể hỗ trợ giám sát rủi ro. | Cơ sở sử dụng dữ liệu phục vụ chống gian lận/AML | W2 Điều 8. Cao đối với quyền được phép và mục đích, không phải bằng chứng rằng mọi trường dữ liệu đều được dùng trong mọi quyết định. |
| W-C6 | Tiền hoàn trả trước hết được dùng để thanh toán các khoản còn nợ theo quy tắc; phần dư có thể được trả về số dư ví. | Hạch toán hoàn tiền; có thể liên quan đến rủi ro | W1 §6.2. Cách thức vận hành đã được ghi nhận; mục đích chống gian lận là suy luận, không phải tuyên bố rõ ràng. |

Hạn mức tín dụng, lãi suất, việc tra cứu/báo cáo thông tin tín dụng và thực thi nghĩa vụ trả nợ chủ yếu liên quan đến rủi ro tín dụng. Không được coi chúng là bằng chứng về báo cáo giao dịch đáng ngờ trong AML. Hợp đồng nêu rõ cả việc đánh giá khả năng trả nợ và các mục đích phòng, chống tội phạm tài chính; những chức năng này có dữ liệu giao nhau nhưng khác nhau về mục tiêu. [W1, W2]

### Vay tiền được cho phép khác với rút tiền qua giao dịch giả

Các đoạn trích nguồn ngắn:

- W1 §3.4: “分付转账功能正在逐步开放中” — “Tính năng chuyển tiền Fenfu đang dần được mở.” (Bản dịch.)
- Định nghĩa tín dụng sau tiêu dùng trong W2: “本人同名收款账户” — “tài khoản nhận tiền đứng tên chính người vay.” (Bản dịch.)

Nhận định khái quát trước đây rằng Fenfu không bao giờ cho phép chuyển tiền hoặc giải ngân vào tài khoản ngân hàng không còn đứng vững trước các nguồn này. Việc vay tiền được cho phép vẫn phải tuân thủ mục đích sử dụng được phép và phụ thuộc vào tính năng thực tế có sẵn. Các giao dịch giả nhằm chuyển tín dụng mua hàng thành tiền mặt bị cấm riêng; không được đánh đồng chúng với quy trình sản phẩm được cho phép và mô tả rõ ràng. [W1–W3]

## Kiểm soát ở lớp thanh toán: có liên quan nhưng không riêng cho Fenfu

| Nhận định | Biện pháp kiểm soát được công bố | Phạm vi / giới hạn |
|---|---|---|
| W-P1 | Thông tin danh tính thật, bản sao giấy tờ khi được yêu cầu và xác minh lại; từ chối/hạn chế nếu không cung cấp thông tin AML thiết yếu. | Chính sách quyền riêng tư Tenpay, W5 §2.1. Áp dụng trên toàn nền tảng. |
| W-P2 | Xác thực giao dịch theo mức độ rủi ro có thể dùng mật khẩu, mã dùng một lần (OTP), chứng thư hoặc cơ chế sinh trắc học tùy chọn. Khôi phục/bỏ phong tỏa/gỡ hạn chế tài khoản có thể yêu cầu thêm bằng chứng về danh tính hoặc giao dịch. | W5 §2.3. Hỗ trợ phòng vệ trước hành vi chiếm đoạt tài khoản; không có bằng chứng về một luồng xác thực bắt buộc duy nhất cho Fenfu. |
| W-P3 | Dữ liệu thiết bị/mạng/hành vi và giao dịch hỗ trợ quản lý rủi ro, thẩm tra AML, giám sát giao dịch và ngăn ngừa hoạt động bất hợp pháp. Thông tin rủi ro cần thiết có thể được trao đổi với các đối tác tài chính liên quan. | W5 §§2, 5, 6. Đây là các mục đích xử lý được công bố, không phải đặc tả mô hình. |
| W-P4 | Điều khoản dành cho thương nhân cho phép xác minh hoạt động kinh doanh/danh tính, giám sát giá trị/số lượng/loại/thời điểm/tần suất giao dịch và các đối tác giao dịch, đồng thời can thiệp khi hoạt động không phù hợp với hồ sơ kinh doanh. | W6 §§3.6–3.10, 4.1. Thỏa thuận thương nhân phiên bản v4 có thể truy cập này chưa có ngày hiệu lực hiện hành được xác minh; dùng làm bằng chứng về điều khoản được công bố, không coi là hợp đồng mới nhất áp dụng phổ biến. |
| W-P5 | Biện pháp ứng phó rủi ro thương nhân bao gồm trì hoãn quyết toán, hạn chế nhận tiền, đình chỉ thanh toán hoặc đóng các giao diện kết nối; thương nhân phải cung cấp bằng chứng giao dịch và có thể bị chấm dứt dịch vụ/báo cáo do hoạt động bị cấm. | W6 §§3.8, 3.10, 4.12. Đây là kiểm soát thương nhân ở cấp nền tảng, không phải kết quả riêng của Fenfu hay quy tắc tự động nộp báo cáo giao dịch đáng ngờ (STR). |

Điểm cần cân bằng về quyền riêng tư: xóa một hóa đơn khỏi giao diện hoặc đóng tài khoản không nhất thiết đồng nghĩa với xóa dữ liệu ở hệ thống phía sau. W5 nêu rõ việc lưu giữ hồ sơ khi pháp luật yêu cầu và mô tả mã hóa, kiểm soát truy cập cùng khử định danh. Báo cáo không nên hứa hẹn việc xóa dữ liệu trái với nghĩa vụ lưu giữ hồ sơ AML.

## Quản trị AML cấp tập đoàn: đã được ghi nhận, không phải công bố mô hình Fenfu

Chính sách AML cấp tập đoàn của Tencent mô tả việc nhận biết/xác minh khách hàng dựa trên rủi ro, thẩm tra tăng cường đối với khách hàng có rủi ro cao hơn, bao gồm người có ảnh hưởng chính trị (PEP) và người liên quan, giám sát/báo cáo hoạt động đáng ngờ cho cơ quan quản lý, kiểm tra độc lập, đào tạo và lưu giữ hồ sơ. [W7]

Báo cáo ESG năm 2024 (công bố tháng 4 năm 2025), trang in số 92, mô tả quản trị AML/tuân thủ các lệnh trừng phạt (sanctions) ở cấp tập đoàn, các cơ cấu tương ứng trong các pháp nhân tài chính được cấp phép và những cải tiến sử dụng dữ liệu lớn cùng học máy. Nội dung này cho thấy cơ chế quản trị và định hướng kỹ thuật được công bố; nó không chứng minh Fenfu đang triển khai một mạng nơ-ron đồ thị (GNN)/mô hình ngôn ngữ lớn (LLM), đồ thị giao dịch, nhà cung cấp danh sách hoặc mô hình cụ thể. Báo cáo cũng đề cập các hoạt động phi tài chính như trò chơi/phát trực tiếp; không được gắn lại nhãn cho những ví dụ đó thành các triển khai BNPL. [W8]

Rà soát bởi con người: các kênh chăm sóc khách hàng và việc xác minh danh tính trong quá trình tương tác dịch vụ đã được ghi nhận, cũng như cơ chế quản trị tuân thủ AML và kiểm tra độc lập. Các nguồn công khai không xác lập quy trình chính xác của điều tra viên Fenfu, người phê duyệt từng báo cáo giao dịch đáng ngờ hay kết quả khiếu nại. Ngược lại, việc “bộ phận chăm sóc khách hàng không thể thay đổi kết quả xét điều kiện theo thời gian thực” không chứng minh toàn bộ quy trình AML vận hành tự chủ. [W1, W2, W7, W8]

## Danh mục nguồn

Tất cả được truy xuất ngày 31 tháng 10 năm 2026. Các ngày dưới đây là ngày của tài liệu, không được suy ra từ đoạn trích kết quả tìm kiếm.

| ID | Nguồn | Ngày/phiên bản | Nội dung thực tế đã đọc |
|---|---|---|---|
| W1 | [Hướng dẫn sử dụng Fenfu chính thức](https://pay.weixin.qq.com/doc/user/4021837995) | Cập nhật ngày 15 tháng 6 năm 2026 theo nội dung trang | Toàn bộ hướng dẫn sản phẩm: điều kiện, hạn chế, chuyển tiền, vay tiền, cập nhật giấy tờ định danh, hoàn tiền, tín dụng, thông tin liên hệ đối tác. |
| W2 | [PDF hợp đồng dịch vụ tín dụng Fenfu của JinCheng](https://www.jccfc.com/api/console/download?file=/volume_gfs/jccfc-www/prod/%E5%88%86%E4%BB%98%E6%8E%88%E4%BF%A1%E6%9C%8D%E5%8A%A1%E5%90%88%E5%90%8CV7.0_20250409_587.pdf) | V7.0; tên tệp chứa 20250409, không phải ngày hiệu lực đã được xác minh riêng | Văn bản trích xuất; đã xem xét kỹ các định nghĩa và Điều 3, 4, 8. Danh tính bên cho vay được nêu rõ ở trang đầu. |
| W3 | [PDF công bố hợp tác Fenfu của DBS](https://www.dbs.com.cn/iwov-resources/doc/footer/Payment_Installment_Service_Description.pdf) | Ngày 9 tháng 9 năm 2026, được ghi tại phần ký trong tài liệu | Toàn bộ công bố ngắn: các pháp nhân đối tác, phân bổ vốn, điều kiện, mục đích, kênh dịch vụ. |
| W4 | [Thỏa thuận WeChat Pay Score](https://posts.tenpay.com/posts/54ad1eea621dc621139fbaa805165f3b.html) | Phiên bản ngày 27 tháng 8 năm 2026 | Toàn bộ thỏa thuận; §§1–3 và 6.2 phân biệt điểm số/tiện ích của thương nhân với tín dụng. |
| W5 | [Chính sách quyền riêng tư Tenpay](https://www.tenpay.com/v3/helpcenter/low/privacy.shtml) | Không có ngày hiệu lực được xác minh trong trang trích xuất | Các phần về danh tính, xác thực, dữ liệu thiết bị/giao dịch, sử dụng/chia sẻ phục vụ quản lý rủi ro, xóa/lưu trữ. |
| W6 | [Thỏa thuận dịch vụ thương nhân WeChat Pay](https://pay.weixin.qq.com/static/protocol/protocol_normal_v4.shtml) | URL v4; chưa xác minh khả năng áp dụng hiện tại | Các điều khoản về nhận biết thương nhân, giám sát, trì hoãn quyết toán và hoạt động bị cấm. |
| W7 | [Tuyên bố chính sách AML của Tencent](https://www.tencent.com/tencent-anti-money-laundering-policy-statement/) | Tuyên bố công khai không ghi ngày | Toàn bộ chính sách ngắn cấp tập đoàn. |
| W8 | [Báo cáo ESG năm 2024 của Tencent](https://static.www.tencent.com/uploads/2025/04/08/7ef7e3b3749bfcbbeccbcc837b794e60.pdf) | Năm báo cáo 2024; công bố tháng 4 năm 2025 | PDF trích xuất; phần AML ở trang in số 92 và bối cảnh rủi ro ở trang 78. Không khẳng định đã xem xét mọi trang. |
| W9 | [Danh mục công bố khoản vay tiêu dùng trực tuyến của DBS](https://www.dbs.com.cn/treasures-sc/personal_online_consumer_credit_loan.page) | Danh mục hiện tại không ghi ngày | Các mục hợp tác và liên kết đến W3. |

Giới hạn của PDF: TinyFish trích xuất văn bản thành công nhưng tạo ra các chỗ xuống dòng. Chưa kiểm tra ảnh trang. Sử dụng tiêu đề điều khoản và tham chiếu số trang in, không suy đoán về bố cục. W2 là hợp đồng công khai của đối tác với các trường thông tin người vay để trống, không phải thỏa thuận hiện hành đã ký của mọi khách hàng. W3 là một công bố hợp tác cụ thể có ghi ngày. Bên cho vay thực tế, tính năng có sẵn và thỏa thuận có hiệu lực của từng người dùng phải được kiểm tra trong hồ sơ tài khoản của họ.

## Khoảng trống và kết luận nghiên cứu

Các nguồn công khai chứng minh có nhiều lớp kiểm tra danh tính, đánh giá giao dịch, hạn chế mục đích sử dụng, phối hợp giữa bên cho vay và đơn vị thanh toán, sử dụng thông tin rủi ro và quản trị AML cấp tập đoàn. Chúng không tiết lộ đặc trưng đầu vào/trọng số mô hình Fenfu, ngưỡng cảnh báo, tỷ lệ tổn thất do gian lận, tỷ lệ dương tính giả, cam kết thời gian xử lý điều tra (SLA) hiện hành, độ chính xác phát hiện AML riêng của sản phẩm hoặc số lượng báo cáo nội bộ. Những khẳng định rằng Fenfu chắc chắn sử dụng nội dung trò chuyện mạng xã hội, GNN, tác tử LLM hoặc các ngưỡng đồ thị cụ thể chưa được xác lập ở đây.

Suy luận thực tiễn cho một nguyên mẫu: mô hình hóa riêng bên cho vay, đơn vị vận hành thanh toán, người dùng và thương nhân; đưa trạng thái danh tính, bối cảnh giao dịch và chính sách về mục đích sử dụng được phép xuyên suốt một quy trình có thể kiểm toán. Tách biệt quyết định chống gian lận với phê duyệt tín dụng và việc chuyển hồ sơ AML lên cấp xử lý cao hơn. Đây là suy luận thiết kế từ các biện pháp kiểm soát công khai, không phải kiến trúc nội bộ của Tencent.
