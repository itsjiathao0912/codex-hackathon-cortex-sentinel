# Cách Alipay/Huabei và WeChat/Fenfu xử lý rủi ro fraud và AML

[Bản tiếng Anh](../README.md)

Ngày nghiên cứu: **31/10/2026**. Phạm vi địa lý: **Trung Quốc đại lục**. Báo cáo tổng hợp bằng chứng công khai về tín dụng tiêu dùng phục vụ mua hàng và các tính năng tín dụng liên quan; đây không phải cuộc kiểm toán hệ thống nội bộ hoặc ý kiến pháp lý toàn diện.

Thuật ngữ dùng trong bản dịch: **BNPL** — mua trước trả sau; **fraud** — gian lận; **AML** — phòng, chống rửa tiền; **credit risk** — rủi ro tín dụng; **CDD** — thẩm tra khách hàng; **merchant** — đơn vị bán hàng/đơn vị chấp nhận thanh toán. Các thuật ngữ kỹ thuật cần thiết được giữ lại bằng tiếng Anh để tiện đối chiếu.

## Các phát hiện chính

1. **Phân biệt ví thanh toán với bên cho vay.** Alipay và WeChat Pay là giao diện/hệ sinh thái thanh toán. Khoản vay thực tế có thể do công ty tài chính tiêu dùng, đơn vị cho vay nhỏ hoặc ngân hàng đối tác cung cấp. Hợp đồng vay xác định bên cho vay chịu trách nhiệm. Không mặc định chỉ có một bên cho vay cho toàn bộ sản phẩm hoặc mọi khoản tín dụng liên quan đến WeChat đều do WeBank cung cấp.
2. **Các nguồn này không xác lập một “điểm fraud/AML” duy nhất.** Nhận diện/xác thực, thẩm định tín dụng, giới hạn giao dịch/merchant, giám sát liên tục và điều tra/báo cáo AML là những chức năng khác nhau. Chúng có thể chia sẻ thông tin nhưng không nhất thiết có cùng mục tiêu hay cùng quyết định.
3. **Phạm vi sản phẩm đã thay đổi.** Công bố hiện tại của Huabei bao gồm khoản vay tiêu dùng bằng tiền mặt được phép. Hướng dẫn Fenfu tháng 6/2026 mô tả tính năng chuyển tiền đang được mở dần và thử nghiệm vay chuyển vào tài khoản ngân hàng, bên cạnh tín dụng phục vụ tiêu dùng. Những tính năng này khác với giao dịch mua hàng giả tạo để lách giới hạn sản phẩm.
4. **Bằng chứng công khai cho thấy nhiều lớp kiểm soát, nhưng chưa xác minh được kiến trúc mô hình nội bộ.** Hợp đồng/hướng dẫn công bố các bước kiểm tra, mục đích xử lý dữ liệu và biện pháp có thể áp dụng. Tuyên bố AI/AML ở cấp tập đoàn không xác lập mô hình nào đang chạy trong một sản phẩm BNPL cụ thể, tần suất sai sót, hoặc liệu mọi trường dữ liệu được liệt kê có được dùng trong từng quyết định hay không.
5. **Báo cáo AML là quy trình riêng, có trách nhiệm giải trình.** Quy định báo cáo áp dụng yêu cầu con người phân tích và lưu hồ sơ về kết quả xử lý cảnh báo giám sát. Tự động tạo cảnh báo hoặc chuẩn bị báo cáo không chứng minh quyết định gửi báo cáo được thực hiện hoàn toàn tự động.

## 1. Những sản phẩm và pháp nhân nào đang được so sánh?

| Hệ sinh thái | Phạm vi sản phẩm | Ranh giới pháp nhân và bằng chứng |
|---|---|---|
| Alipay / Ant | Huabei (花呗): tín dụng tiêu dùng quay vòng, tính năng mua hàng/trả góp và hình thức tín dụng tiền mặt được mô tả riêng trong công bố tháng 7/2026 | Ant Consumer Finance công bố thông tin sản phẩm hiện tại. Hợp đồng Huabei có thể truy cập công khai phân biệt bên cung cấp tín dụng với vai trò thanh toán của Alipay, nhưng chứa nội dung về nhà cung cấp không có ngày/thuộc phiên bản cũ. Đây không phải danh sách đầy đủ các bên cho vay hiện tại. [A-S1, A-S2] |
| WeChat | Fenfu (分付): mặc định là tín dụng tiêu dùng tính lãi theo ngày, có ưu đãi trả góp tại một số merchant và các tính năng bổ sung tùy điều kiện đủ tiêu chuẩn | Một hợp đồng công khai nêu JinCheng Consumer Finance là bên cho vay, Tenpay là đơn vị vận hành thanh toán và Weiheng là đơn vị tư vấn công nghệ/dịch vụ. Một công bố khác có ngày của DBS mô tả cơ chế đồng cho vay khác. Không tài liệu nào mô tả khoản vay của tất cả khách hàng. [W1–W3] |

**Không đồng nhất Fenfu với WeChat Pay Score hoặc Weilidai.** Pay Score là sản phẩm dịch vụ merchant riêng; thỏa thuận tháng 8/2026 giới hạn việc sử dụng cho dịch vụ tài trợ/tín dụng. Hướng dẫn Fenfu phân biệt Fenfu với Weilidai. Điểm số được dùng để miễn tiền đặt cọc không tự động trở thành đầu vào thẩm định khoản vay tiêu dùng đã được tài liệu xác nhận. [W1, W4, W9]

Nguồn gốc về sản phẩm: [Công bố của Ant Consumer Finance](https://www.myxiaojin.cn/notice/detail/6), [Hướng dẫn Fenfu](https://pay.weixin.qq.com/doc/user/4021837995), [Công bố hợp tác của DBS](https://www.dbs.com.cn/iwov-resources/doc/footer/Payment_Installment_Service_Description.pdf). Cần đối chiếu hợp đồng hiện hành trong tài khoản khách hàng để xác định chính xác điều khoản nào áp dụng và tính năng nào khả dụng.

## 2. So sánh các lớp kiểm soát

Các nhãn: **PRODUCT** = tài liệu cho sản phẩm được nêu tên; **PLATFORM** = hệ sinh thái thanh toán rộng hơn; **GROUP** = tuyên bố cấp tập đoàn; **REQUIREMENT** = nghĩa vụ pháp lý, không phải bằng chứng đã triển khai. Hợp đồng không ghi ngày xác lập nội dung được viết trong đó, không chứng minh đó là thỏa thuận đang áp dụng cho mọi khách hàng hiện nay.

| Giai đoạn kiểm soát | Bằng chứng Alipay / Huabei | Bằng chứng WeChat / Fenfu | Kết luận có thể đưa ra |
|---|---|---|---|
| Danh tính và tiếp nhận khách hàng | Hợp đồng Huabei công khai yêu cầu thông tin trung thực và xác minh danh tính. **PRODUCT; chưa chắc chắn về phiên bản** [A-S2] | Hướng dẫn yêu cầu danh tính thật, thẻ ngân hàng tại Trung Quốc đại lục và tài khoản thanh toán ở trạng thái bình thường. Việc cập nhật giấy tờ định danh được liên hệ rõ với nghĩa vụ AML. **PRODUCT** [W1] | Cả hai đều công bố kiểm soát danh tính. Trong các tài liệu hiện hành đã đọc, hướng dẫn Fenfu cung cấp mối liên hệ trực tiếp này với AML liên tục. Điều đó không chứng minh bên nào hiệu quả hơn. |
| Lạm dụng tài khoản / xác thực | Hợp đồng Huabei có nội dung bảo vệ thông tin xác thực và thông báo hành vi mạo danh. Chưa xác minh được cách triển khai sinh trắc học/thiết bị cụ thể cho BNPL hiện tại. [A-S2] | Chính sách quyền riêng tư Tenpay mô tả xác thực theo rủi ro và xác minh bổ sung khi khôi phục tài khoản. **PLATFORM**, không phải luồng xác thực chung cho mọi trường hợp Fenfu [W5] | Xác thực hỗ trợ chống lạm dụng tài khoản. Bằng chứng công khai chưa đủ để so sánh tỷ lệ phát hiện chiếm đoạt tài khoản (account takeover). |
| Phê duyệt tín dụng và hạn mức | Hợp đồng công khai có thẩm định rủi ro và thay đổi hạn mức. [A-S2] | Hướng dẫn và hợp đồng đối tác có điều kiện đủ tiêu chuẩn, hạn mức, lãi suất, trả nợ và hồ sơ tín dụng. [W1–W3] | Chủ yếu xử lý credit risk; giảm hạn mức không tự động là quyết định AML. |
| Tính xác thực của giao dịch và mục đích được phép | Hợp đồng công khai cấm đơn hàng giả/rút tiền qua giao dịch giả tạo, cho phép tạm dừng vì lý do an toàn và sử dụng thông tin giao dịch/hoàn tiền/tranh chấp. **PRODUCT; chưa chắc chắn về phiên bản** [A-S2] | Hướng dẫn mô tả đánh giá hệ thống theo thời gian thực; hợp đồng đối tác cấm đơn hàng giả và cash-out trái phép, đồng thời cho phép hạn chế tạm thời. **PRODUCT / riêng đối tác** [W1, W2] | Cả hai đều công bố kiểm soát việc sử dụng sai tín dụng tiêu dùng. Chưa biết chính xác đầu vào mô hình và các ngưỡng. |
| Kiểm soát merchant | Hợp đồng merchant có xác minh danh tính/hoạt động kinh doanh, trao đổi thông tin rủi ro, giới hạn, tạm dừng và trì hoãn thanh toán tiền cho merchant. **PLATFORM; không có ngày** [A-S3] | Thỏa thuận merchant có kiểm tra merchant, hoạt động không phù hợp hồ sơ kinh doanh, trì hoãn thanh toán và hạn chế. **PLATFORM; chưa xác minh phiên bản hiện hành** [W6] | Kiểm soát merchant/đơn vị thanh toán cho merchant bổ sung cho kiểm soát phía người vay. Các điều khoản không chứng minh mọi biện pháp được áp dụng giống nhau cho từng giao dịch BNPL. |
| Giám sát tội phạm tài chính liên tục | Ant mô tả quản trị chỉ báo ở cấp tập đoàn và tự động hóa AML/báo cáo. **GROUP, doanh nghiệp tự công bố** [A-S4] | Hợp đồng đối tác Fenfu cho phép xử lý dữ liệu danh tính, giao dịch, dòng tiền và thiết bị/mạng liên quan nhằm phục vụ AML/chống lừa đảo; chính sách Tencent mô tả giám sát/báo cáo. **Quyền xử lý dữ liệu ở cấp PRODUCT + chính sách GROUP** [W2, W7] | Có bằng chứng về mục đích giám sát và quản trị. Quyền xử lý dữ liệu không phải đặc tả mô hình hoặc bằng chứng về hiệu quả phát hiện. |
| Rà soát và báo cáo | Bằng chứng công khai chưa đủ để mô tả lại quy trình rà soát vụ việc/phê duyệt gửi báo cáo của Huabei. | Bằng chứng công khai chưa đủ để mô tả lại quy trình điều tra hoặc chuỗi phê duyệt gửi báo cáo của Fenfu. | Quy định áp dụng yêu cầu con người phân tích cảnh báo và ghi lý do báo cáo/loại trừ. **REQUIREMENT** [R3]. Không biến nghĩa vụ này thành khẳng định đã quan sát được cách nhà cung cấp triển khai. |
| Quản trị dữ liệu | Hợp đồng merchant có điều khoản về thông tin xác thực/an toàn/bảo mật; chưa xác minh được danh mục đầy đủ về xử lý dữ liệu riêng tư hiện tại của Huabei. [A-S3] | Chính sách Tenpay có xử lý dữ liệu phục vụ rủi ro, bảo mật và lưu giữ theo pháp luật. **PLATFORM** [W5] | Xóa trên giao diện không chứng minh dữ liệu đã được xóa ở backend. Cần xét đồng thời nghĩa vụ lưu hồ sơ và quyền riêng tư. |

## 3. Cách hiểu vòng đời kiểm soát

Đây là **mô hình phân tích tổng hợp từ các biện pháp đã công bố**, không phải kiến trúc hệ thống thực tế bị tiết lộ hoặc được tái dựng đầy đủ.

1. **Xác định khách hàng và các pháp nhân chịu trách nhiệm.** Phân biệt tài khoản thanh toán với quan hệ cho vay và điều khoản sản phẩm áp dụng.
2. **Xác thực và đánh giá quyền sử dụng.** Kiểm soát danh tính và tính toàn vẹn tài khoản xử lý mạo danh/lạm dụng tài khoản; điều kiện tín dụng xác định khả năng được vay.
3. **Đánh giá giao dịch dự kiến.** Mục đích sản phẩm, tính xác thực của giao dịch và bối cảnh merchant có thể ảnh hưởng việc cho phép tiếp tục. Danh tính thật không bảo đảm giao dịch là thật.
4. **Áp dụng biện pháp tương xứng.** Có thể từ chối thanh toán, yêu cầu thêm bằng chứng, hạn chế dịch vụ hoặc trì hoãn thanh toán cho merchant khi điều khoản/pháp luật áp dụng cho phép. Những biện pháp này không đồng nghĩa với phong tỏa tài sản theo thẩm quyền pháp luật.
5. **Tiếp tục giám sát sau thanh toán.** Hồ sơ hoàn tiền, tranh chấp, trả nợ và dòng tiền có thể phục vụ các chức năng quản trị rủi ro khác nhau. Không được trình bày riêng cơ chế hạch toán hoàn tiền như một thuật toán AML đã được chứng minh.
6. **Rà soát hoạt động đáng ngờ theo quy trình riêng.** Giám sát AML dẫn đến phân tích có lưu hồ sơ và, khi có cơ sở, báo cáo do tổ chức chịu trách nhiệm thực hiện. Tách biệt bằng chứng và quyết định này với quyết định chăm sóc khách hàng hoặc tín dụng.
7. **Duy trì hồ sơ và cập nhật thẩm tra.** Quy định áp dụng yêu cầu rà soát liên tục và lưu giữ hồ sơ; nghĩa vụ pháp luật không chứng minh chất lượng triển khai của từng nhà cung cấp. [R1–R3]

### Bốn ví dụ giúp tránh nhầm nhóm rủi ro

- **Sử dụng tài khoản không được phép:** vấn đề fraud về danh tính/xác thực, kể cả khi khoản vay được trả đủ.
- **Giao dịch mua hàng giả tạo tại merchant:** vấn đề sử dụng bị cấm/fraud; cần thêm bằng chứng để xác định có cả vấn đề AML hay không.
- **Tính năng chuyển tiền hoặc vay tiền mặt được phép:** bản thân không phải gian lận hay rửa tiền. Cần xác minh mục đích sử dụng được phép của đúng sản phẩm.
- **Người vay thật nhưng không có khả năng trả nợ:** chủ yếu là credit risk/rủi ro không trả được nợ. Chậm trả nợ riêng lẻ không chứng minh fraud hoặc rửa tiền.

Xem [phân loại rủi ro](RISK-TAXONOMY.md) để phân biệt fraud, tín dụng, AML, vận hành và quản trị dữ liệu.

## 4. Thực sự biết được gì về AI và công nghệ phát hiện?

**Ant:** thông cáo do doanh nghiệp phát hành tháng 7/2025 mô tả các chỉ báo AML thống nhất, RiskKey/iGuardian và tự động hóa, đồng thời đề cập năng lực liên quan đến AI. Đây là công bố của doanh nghiệp trong phạm vi kinh doanh rộng hơn. Nó không xác lập Huabei sử dụng từng thành phần được nêu tên hoặc một LLM tự quyết định gửi báo cáo. Bài viết Tân Hoa Xã tháng 6/2026 đưa tin về đánh giá rủi ro theo ngữ cảnh, theo thời gian thực của Ant Consumer Finance, nhưng chưa truy xuất được báo cáo phát triển bền vững gốc; cần coi đây là nguồn thứ cấp thuật lại công bố của doanh nghiệp. [A-S4, A-S5]

**Tencent:** chính sách AML và báo cáo ESG 2024 mô tả quản trị dựa trên rủi ro, thẩm tra trường hợp rủi ro cao hơn, báo cáo, kiểm tra/đào tạo và sử dụng big data/machine learning. Những tài liệu này hỗ trợ mô tả ở cấp tập đoàn, không xác lập riêng Fenfu sử dụng graph neural networks, LLM agents, nội dung trò chuyện mạng xã hội, trọng số mô hình cụ thể hoặc đạt độ chính xác phát hiện cụ thể. [W7, W8]

**Kết luận:** tài liệu công khai cho thấy sự kết hợp giữa chính sách, kiểm tra danh tính, đánh giá rủi ro, giám sát và rà soát. Chúng chưa đủ để so sánh chính xác “thuật toán fraud của họ là gì”. Việc một bên công bố chi tiết hơn về quyền xử lý dữ liệu không phải bằng chứng bên đó kiểm soát tốt hơn.

## 5. Bối cảnh pháp lý và giới hạn về đánh giá hiệu quả vận hành

Luật AML sửa đổi có hiệu lực từ tháng 1/2025. Quy định CDD có hiệu lực từ tháng 1/2026 nêu rõ phạm vi gồm công ty tài chính tiêu dùng và tổ chức thanh toán phi ngân hàng, đồng thời có các điều khoản liên quan áp dụng cho đơn vị cho vay nhỏ trực tuyến. Sửa đổi về báo cáo có hiệu lực từ tháng 12/2025 yêu cầu rõ việc con người phân tích và lưu lý do báo cáo hoặc loại trừ cảnh báo giám sát. Những nguồn này xác lập nghĩa vụ, không phải cuộc kiểm toán nhà cung cấp. [R1–R3]

Các quy định đã xác minh trong nghiên cứu yêu cầu lưu giữ ít nhất mười năm đối với hồ sơ danh tính/giao dịch liên quan, với phạm vi và mốc tính thời gian do quy định xác định; không dùng lại mô tả chung cũ về thời hạn năm năm. Biện pháp quản trị rủi ro khách hàng cũng phải tuân thủ yêu cầu tương xứng và giới hạn về phong tỏa tài sản. Xem [kết quả nghiên cứu pháp lý](regulatory-findings.md) để biết đầy đủ nguồn dẫn, thời điểm và điều kiện áp dụng.

Lịch sử xử lý vi phạm cho thấy tuyên bố công nghệ ấn tượng không chứng minh hệ thống kiểm soát hoàn hảo. Tổng mức xử phạt Ant năm 2023 bao gồm nhiều nhóm vi phạm, không phải mức phạt riêng Huabei hoặc chỉ riêng AML. Công bố của Tencent về Tenpay liên quan vi phạm dịch vụ thanh toán trong quá khứ và tuyên bố khắc phục của ban lãnh đạo; đây không phải kết luận riêng về Fenfu. Nghiên cứu này không suy ra hiệu quả sản phẩm hiện tại từ mức phạt hoặc từ tuyên bố đã khắc phục của doanh nghiệp. [R4, R5]

## 6. Những điều vẫn chưa biết

Bằng chứng công khai đã xem xét **chưa xác lập được**:

- Ngưỡng quy tắc đang dùng trong hệ thống thực tế, trọng số đặc trưng của mô hình hoặc kiến trúc dùng chung giữa các sản phẩm.
- Tổn thất do fraud, tỷ lệ false positive/false negative hoặc độ chính xác phát hiện AML riêng cho BNPL.
- Hàng đợi phân luồng cảnh báo, nhân sự điều tra, SLA xử lý vụ việc hoặc số lượng báo cáo cụ thể.
- Danh sách đầy đủ bên cho vay hiện tại và hợp đồng đang áp dụng cho mọi khách hàng.
- Danh mục đầy đủ hiện tại về quyền riêng tư/lưu giữ dữ liệu của Huabei hoặc báo cáo phát triển bền vững gốc của Ant Consumer Finance đứng sau nguồn thứ cấp.
- Liệu một năng lực AI được nêu tên có được triển khai trong đúng sản phẩm/phiên bản mà một người vay cụ thể sử dụng hay không.

Bằng chứng nên thu thập tiếp nếu có thể truy cập: hợp đồng vay và thông báo quyền riêng tư tương ứng trong ứng dụng; tài liệu sản phẩm của bên cho vay hiện tại; công bố kiểm soát của cơ quan quản lý hoặc đã được bảo đảm độc lập; và báo cáo kỹ thuật gốc có nêu phạm vi triển khai. Không yêu cầu thông tin đăng nhập của khách hàng hoặc dữ liệu giao dịch nhạy cảm thực tế chỉ để lấp các khoảng trống này.

## 7. Tài liệu bằng chứng và phương pháp

Việc tìm kiếm và truy xuất bằng TinyFish được thực hiện theo ba nhánh. **19 tài liệu nguồn riêng biệt đã được xem xét nội dung thực chất**: năm tài liệu về Ant/Huabei, chín về WeChat/Fenfu và năm về bối cảnh pháp lý. Với báo cáo dài, các phần liên quan đã được đọc; con số này không có nghĩa mọi trang của mọi báo cáo đều đã được đọc. Mười tám nguồn là tài liệu chính thức/do bên phát hành cung cấp hoặc bản đăng lại chính thức, và một nguồn là bài báo thứ cấp. Không tính các lần truy xuất thất bại hoặc đầu mối chỉ xuất hiện trong kết quả tìm kiếm.

- [Kết quả Alipay/Huabei và danh mục năm nguồn](alipay-findings.md)
- [Kết quả WeChat/Fenfu và danh mục chín nguồn](wechat-findings.md)
- [Kết quả pháp lý và danh mục năm nguồn](regulatory-findings.md)
- [Phạm vi và nguyên tắc bằng chứng](RESEARCH-SCOPE.md)
- [Phân loại rủi ro](RISK-TAXONOMY.md)

Quy ước trích dẫn: A-S1–A-S5 tương ứng S1–S5 trong báo cáo Alipay; W1–W9 và R1–R5 tương ứng danh mục nguồn của báo cáo WeChat và pháp lý. Mỗi danh mục ghi ngày, phạm vi và giới hạn truy xuất. Hướng dẫn và hợp đồng sản phẩm là bằng chứng về hành vi/quyền được công bố, không phải chứng nhận độc lập về hiệu quả vận hành.
