---
title: "Worklog Tuần 5"
date: 2026-05-15
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Mục tiêu tuần 5: Định hình tư duy FinOps trong phát triển phần mềm

Bước sang tuần thứ 5, mục tiêu cốt lõi không chỉ dừng lại ở việc vận hành hạ tầng mà là làm chủ bài toán kinh tế trên Cloud. Đối với một lập trình viên, việc thiết kế một hệ thống mạnh mẽ là chưa đủ nếu nó ngốn quá nhiều ngân sách. Tuần này tập trung vào việc xây dựng "hệ thống phòng thủ tài chính" thông qua các mục tiêu chi tiết:

- **Khám phá triết lý quản trị tài chính (FinOps):** Tìm hiểu tổng quan về cách quản lý chi phí trên AWS bằng dịch vụ AWS Budgets. Hiểu sâu vai trò của nó không chỉ ở việc theo dõi, mà còn trong việc kiểm soát chủ động và cảnh báo chi phí sử dụng dịch vụ AWS.
- **Làm chủ các phương pháp triển khai ngân sách:** Thực hành tạo Budget bằng template có sẵn để thiết lập ngân sách một cách nhanh chóng và chuẩn xác.
- **Phân tách các lớp giám sát:** 
  - Tạo Cost Budget để theo dõi trực tiếp dòng tiền chi phí sử dụng AWS theo chu kỳ tháng.
  - Tạo Usage Budget để giám sát mức độ sử dụng tài nguyên AWS, đặc biệt nhắm vào các dịch vụ tính phí theo thời gian chạy (như EC2).
- **Tiếp cận mô hình tối ưu chi phí doanh nghiệp:** Tìm hiểu Reservation Budget để giám sát mức độ sử dụng của các máy chủ Reserved Instances, đồng thời tìm hiểu Savings Plans Budget để đánh giá mức độ sử dụng của các gói Savings Plans.
- **Xây dựng hệ thống tự động hóa cảnh báo:** Cấu hình hệ thống alert threshold và thiết lập email notification nhằm đảm bảo người quản trị nhận được cảnh báo ngay khi chi phí hoặc mức sử dụng tiệm cận ngưỡng rủi ro.
- **Phân tích và Bảo trì hệ thống:** Đánh giá độ hiệu quả thông qua việc kiểm tra Budget history, Budget health và các trạng thái cảnh báo. Đồng thời, thực hành dọn dẹp (xóa các Budget đã tạo) sau khi hoàn thành lab để tránh bị làm phiền bởi các thông báo không cần thiết trong tương lai.

---

### Các công việc cần triển khai trong tuần này:

| Thứ | Hạng mục công việc chuyên sâu | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 2 | - **Nghiên cứu nền tảng:** Đọc tổng quan workshop Cost Management with AWS Budgets. <br> - Tìm hiểu vai trò kiến trúc của AWS Budgets trong chiến lược quản lý chi phí AWS. <br> - Truy cập bảng điều khiển trung tâm AWS Billing and Cost Management. <br> - Phân tích và làm quen với giao diện Budgets trong AWS Console. | 01/06/2026 | 01/06/2026 | https://000007.awsstudygroup.com/1-create-budget/ |
| 3 | - **Triển khai Template:** Tạo Budget bằng template có sẵn. <br> - Phân tích lợi ích khi chọn template Monthly cost budget. <br> - Nhập các tham số định danh: tên Budget, số tiền ngân sách hàng tháng và thiết lập ngưỡng cảnh báo. <br> - Đánh giá quá trình bằng cách kiểm tra Budget đã tạo thành công và xem dữ liệu trên Budget history. | 02/06/2026 | 02/06/2026 | https://000007.awsstudygroup.com/1-create-budget/ |
| 4 | - **Tùy biến Cost Budget:** Tạo Cost Budget bằng chế độ Customize để can thiệp sâu vào thông số. <br> - Chọn loại ngân sách Cost budget. <br> - Cấu hình linh hoạt các biến số: Period (chu kỳ), Budget effective dates (ngày hiệu lực), Budgeting method (phương pháp phân bổ) và Budgeted amount (tổng ngân sách). <br> - Cấu hình Budget scope áp dụng toàn diện cho All AWS services và tính toán dựa trên chỉ số Unblended costs. | 03/06/2026 | 03/06/2026 | https://000007.awsstudygroup.com/2-cost-budgets/ |
| 5 | - **Thiết lập chuỗi cảnh báo:** Cấu hình alert threshold cho Cost Budget. <br> - Thêm địa chỉ email nhận cảnh báo tự động khi chi phí vượt ngưỡng. <br> - Thực hiện bước review lại toàn bộ cấu hình Cost Budget. <br> - Tạo Budget và xác nhận trạng thái hoạt động trên hệ thống. | 04/06/2026 | 04/06/2026 | https://000007.awsstudygroup.com/2-cost-budgets/ |
| 6 | - **Kiểm soát dung lượng phần cứng:** Tạo Usage Budget để trực tiếp theo dõi mức sử dụng tài nguyên thay vì tiền tệ. <br> - Chọn Usage budget trong danh mục Budget types. <br> - Cấu hình bộ lọc Usage type groups, tập trung vào ví dụ EC2: ELB - Running Hours. <br> - Thiết lập giới hạn usage hours tối đa và cấu hình alert threshold tương ứng. | 05/06/2026 | 05/06/2026 | https://000007.awsstudygroup.com/3-usage-budget/ |
| 7 | - **Phân tích mô hình cam kết:** Tìm hiểu cơ chế của Reservation Budget áp dụng cho Reserved Instances. <br> - Tìm hiểu cơ chế của Savings Plans Budget áp dụng cho Savings Plans. <br> - Thực hành hoặc xem hướng dẫn cách tạo RI Budget và Savings Plans Budget. <br> - Phân tích cách cấu hình coverage threshold (ngưỡng bao phủ), utilization threshold (ngưỡng tận dụng) và email alert. | 06/06/2026 | 06/06/2026 | https://000007.awsstudygroup.com/4-reservation-budget/ <br> https://000007.awsstudygroup.com/5-saving-plans-budget/ |
| CN | - **Đánh giá và Dọn dẹp:** Kiểm tra toàn diện danh sách Budget đã tạo. <br> - Đọc hiểu các chỉ số từ Budget health và Budget history. <br> - Tiến hành xóa các Budget đã tạo trong quá trình thực hành. <br> - Viết báo cáo ghi nhận kết quả, khó khăn, hướng khắc phục và đúc kết bài học rút ra. | 07/06/2026 | 07/06/2026 | https://000007.awsstudygroup.com/6-clean-up/ |

---

### Kết quả đạt được tuần 5: Khảo sát và Đúc kết lý thuyết

#### 1. Phân tích kiến trúc AWS Budgets & AWS Billing and Cost Management

**Tư duy kiến trúc hệ thống AWS Budgets**
Trong môi trường Cloud, việc cấp phát tài nguyên diễn ra chỉ qua vài dòng code hoặc cú click chuột. Điều này dẫn đến rủi ro "bùng nổ chi phí" nếu không có cơ chế kiểm soát. AWS Budgets ra đời chính là dịch vụ dùng để theo dõi chi phí, mức sử dụng tài nguyên và các cam kết tiết kiệm chi phí trên AWS. Nó cung cấp tính linh hoạt cực cao khi giúp người dùng đặt ngân sách đa dạng theo ngày, tháng, quý hoặc năm. 

Một đặc điểm kiến trúc vô cùng quan trọng mà tôi đúc kết được: Cần chú ý rằng AWS Budgets chỉ cảnh báo, không tự động dừng dịch vụ khi vượt ngân sách. Điều này thoạt nhìn có vẻ là một thiếu sót, nhưng thực chất là thiết kế có chủ đích (by design) của AWS. Nếu một hệ thống backend đang phục vụ hàng ngàn người dùng đột nhiên bị tắt chỉ vì vượt hạn mức vài đô la, thiệt hại về kinh doanh sẽ lớn hơn rất nhiều. Do đó, khi chi phí hoặc mức sử dụng vượt ngưỡng đã cấu hình, AWS Budgets có thể gửi cảnh báo qua email, trao quyền quyết định xử lý sự cố cho con người. Điều này chứng minh AWS Budgets phù hợp với người mới học AWS vì giúp kiểm soát chi phí trong quá trình thực hành lab, đồng thời an toàn cho hệ thống production.

**Giao diện trung tâm AWS Billing and Cost Management**
Đây là trái tim tài chính của tài khoản. Tôi đã biết cách truy cập AWS Billing and Cost Management từ AWS Management Console. Giao diện này không chỉ hiển thị số dư, mà hiểu đây là khu vực quản lý thông tin chi phí, hóa đơn, ngân sách và cảnh báo chi phí. Tại đây, tôi biết sử dụng menu Budgets để tạo, xem, chỉnh sửa hoặc xóa các Budget và biết cách kiểm tra trạng thái Budget sau khi tạo thành công.

#### 2. Chiến lược thiết lập Ngân sách (Template vs. Customize)

**Triển khai nhanh với Template**
Trong nhiều trường hợp, chúng ta chỉ cần một cảnh báo cơ bản. Việc sử dụng template giúp tạo Budget nhanh bằng các cấu hình có sẵn. Bằng cách biết chọn Use a template để sử dụng mẫu đơn giản, cụ thể là biết chọn Monthly cost budget để tạo ngân sách chi phí hàng tháng, tôi tiết kiệm được rất nhiều thao tác. Các trường thông tin chỉ yêu cầu biết nhập Budget name, monthly budget amount và alert threshold. Tuy nhiên, tôi cũng hiểu rằng template phù hợp khi cần thiết lập nhanh cảnh báo chi phí cơ bản, còn đối với hệ thống phức tạp, ta phải đi sâu vào chế độ Customize. Hậu kiểm tra luôn cần thiết bằng cách biết kiểm tra Budget history sau khi tạo Budget thành công.

**Tùy biến chuyên sâu với Cost Budget**
Để có độ hạt phân giải (granularity) cao hơn, Cost Budget dùng để theo dõi chi phí sử dụng AWS thông qua chế độ Customize. Tôi đã nắm vững quy trình biết tạo Cost Budget bằng chế độ Customize và biết chọn Budget type là Cost budget.

Quá trình này đòi hỏi sự am hiểu về các chu kỳ tài chính:
- **Chu kỳ thời gian:** Biết cấu hình Period gồm Daily, Monthly, Quarterly hoặc Annually.
- **Vòng đời ngân sách:** Tôi đã biết phân biệt Recurring Budget và Expiring Budget. Trong đó, Recurring Budget: ngân sách lặp lại theo chu kỳ (dành cho các server chạy liên tục), còn Expiring Budget: ngân sách chỉ áp dụng trong một khoảng thời gian nhất định (cực kỳ lý tưởng cho các đợt test hoặc deploy tính năng mới).
- **Chiến lược cấp phát:** Biết chọn Budgeting method giữa Fixed: ngân sách cố định cho mỗi kỳ và Planned: ngân sách có thể thay đổi theo từng tháng.
- **Phạm vi giám sát:** Biết chọn Budget scope là All AWS services để theo dõi toàn bộ dịch vụ AWS và đặc biệt là biết chọn Aggregate costs by là Unblended costs. Chỉ số Unblended costs phản ánh chi phí thô thực tế ngay tại thời điểm hiện tại, không bị làm nhiễu bởi các thuật toán trung bình hóa chiết khấu, mang lại dữ liệu minh bạch nhất. Cuối cùng, tôi biết thêm alert threshold để nhận cảnh báo khi chi phí đạt một tỷ lệ nhất định của ngân sách.

#### 3. Dịch chuyển góc nhìn từ Chi phí sang Tài nguyên vật lý (Usage Budget)

Việc chỉ nhìn vào dòng tiền đôi khi tạo ra độ trễ trong việc phát hiện lỗi hệ thống (ví dụ một vòng lặp vô tận sinh ra hàng triệu request S3). Do đó, Usage Budget dùng để theo dõi mức sử dụng tài nguyên thay vì số tiền chi phí. Tôi đã phân tích rõ biết điểm khác nhau giữa Cost Budget và Usage Budget: Cost Budget theo dõi chi phí trong khi Usage Budget theo dõi mức sử dụng tài nguyên.

Quy trình thiết lập bao gồm biết chọn Budget type là Usage budget. Chìa khóa ở đây là khả năng phân loại bằng cách biết chọn Usage type groups để xác định loại tài nguyên cần theo dõi. Trong phạm vi lab, Usage Budget có thể dùng để theo dõi EC2: ELB - Running Hours. Bằng cách biết thiết lập giới hạn usage hours cho tài nguyên và biết cấu hình email alert khi mức sử dụng vượt ngưỡng, quản trị viên có thể can thiệp ngay trước khi hóa đơn bị tính. Đúc kết lại, hiểu Usage Budget hữu ích với các dịch vụ tính phí theo giờ như EC2, Load Balancer hoặc các tài nguyên chạy liên tục.

#### 4. Quản lý cam kết dài hạn (Reservation & Savings Plans Budgets)

Mặc dù trong quá trình học tập ít khi mua các gói này, nhưng hiểu biết về chúng là tiêu chuẩn của một kỹ sư Cloud thực thụ.
- **Reservation Budget:** Hiểu Reservation Budget dùng để theo dõi Reserved Instances. Vì Reserved Instances thường yêu cầu cam kết hoặc thanh toán trước nên trong phạm vi lab chỉ nên xem hướng dẫn hoặc thực hành ở mức demo. Ngân sách này giúp quản trị viên biết Reservation Budget giúp theo dõi coverage hoặc utilization của Reserved Instances. Cụ thể, việc biết cấu hình Coverage threshold để theo dõi mức bao phủ của Reserved Instances sẽ cho biết có bao nhiêu phần trăm máy chủ đang chạy được hưởng lợi từ mức giá ưu đãi. Điều này minh chứng Reservation Budget phù hợp với môi trường doanh nghiệp đã sử dụng Reserved Instances để tối ưu chi phí dài hạn.
- **Savings Plans Budget:** Hiểu Savings Plans Budget dùng để theo dõi mức sử dụng Savings Plans. Đây là mô hình linh hoạt hơn, vì Savings Plans là hình thức cam kết sử dụng tài nguyên tính toán trong một khoảng thời gian nhất định để đổi lấy mức giá thấp hơn so với On-Demand. Công cụ này biết Savings Plans Budget giúp theo dõi utilization threshold. Nếu tỷ lệ tận dụng thấp, hệ thống sẽ cảnh báo bằng cách biết cấu hình email alert để nhận thông báo khi mức sử dụng Savings Plans chưa đạt kỳ vọng. Tóm lại, Savings Plans Budget phù hợp khi hệ thống có nhu cầu sử dụng compute ổn định trong thời gian dài.

#### 5. Phân tích Hệ thống Cảnh báo, Health và Kỷ luật Clean Up

- **Hệ thống Alert:** Hiểu alert threshold là ngưỡng cảnh báo được đặt theo phần trăm hoặc giá trị cụ thể. Để xây dựng hệ thống phòng thủ tốt, cần biết cấu hình nhiều mức cảnh báo, ví dụ 50%, 80% và 100% và biết thêm email để nhận cảnh báo ngân sách. Cần quy hoạch rõ rằng người nhận email nên là người có trách nhiệm theo dõi chi phí hoặc quản lý tài khoản AWS và luôn phải biết kiểm tra email xác nhận hoặc thông báo từ AWS Budgets sau khi cấu hình.
- **Chẩn đoán (Health & History):** Hiểu Budget health cho biết trạng thái hiện tại của ngân sách so với mức đã đặt. Để có cái nhìn toàn cảnh, biết dùng Budget history để xem xu hướng chi phí hoặc mức sử dụng theo thời gian và biết quan sát trạng thái ngân sách để đánh giá tài khoản AWS có đang sử dụng vượt mức dự kiến hay không. Một đặc tính kỹ thuật cần lưu ý là dữ liệu chi phí trên AWS có thể có độ trễ, nên cần chờ một khoảng thời gian để số liệu cập nhật đầy đủ.
- **Kỷ luật Dọn dẹp:** Hiểu cleanup là bước cần thiết sau khi hoàn thành lab. Việc biết xóa các Budget đã tạo nếu chỉ dùng để thực hành giúp tránh rác hệ thống. Tôi cũng nắm rõ bản chất kiến trúc rằng xóa AWS Budgets không xóa tài nguyên đang chạy trong AWS account vì AWS Budgets chỉ là công cụ theo dõi và cảnh báo, không phải tài nguyên xử lý ứng dụng. Cuối cùng, luôn biết kiểm tra lại danh sách Budget sau khi xóa để đảm bảo không còn cảnh báo không cần thiết.

---

### Trải nghiệm Thực hành: Phân tích từng bước cấu hình

Quá trình thực hành được chia làm 6 module, đi từ việc khởi tạo cơ bản đến dọn dẹp hệ thống.

**Module 1 — Thiết lập phòng tuyến đầu tiên (Create Budget with Template)**
- Truy cập vào AWS Management Console.
- Tìm kiếm và mở dịch vụ AWS Billing and Cost Management.
- Tại thanh điều hướng, chọn mục Budgets ở menu bên trái.
- Bắt đầu quy trình bằng cách nhấn Create a budget để bắt đầu tạo ngân sách.
- Lựa chọn phương pháp nhanh: Chọn Use a template (simplified).
- Ở đây, tôi chọn template Monthly cost budget vì nó bao phủ tốt nhu cầu hàng tháng.
- Nhập tên Budget theo yêu cầu lab và nhập số tiền ngân sách hàng tháng làm mức giới hạn an toàn.
- Cấu hình alert threshold để nhận cảnh báo khi chi phí đạt ngưỡng.
- Nhấn Create budget để hoàn tất.
- Sau đó, tôi kiểm tra Budget đã được tạo thành công và mở Budget history để xem lịch sử ngân sách. Quá trình này giúp tôi kiểm tra các loại alert có sẵn trong template.

**Module 2 — Chạm vào các thiết lập sâu (Create Cost Budget)**
- Trở lại AWS Billing and Cost Management.
- Chọn Budgets ở menu bên trái và nhấn Create budget.
- Lần này, trong phần Budget setup, chọn Customize để tự tay tinh chỉnh.
- Trong Budget types, chọn Cost budget và nhấn Next để tiếp tục.
- Ở phần Set your budget, nhập Budget name là `Monthly`.
- Tôi chọn Period phù hợp, ví dụ Monthly.
- Tại phần Budget effective dates, tôi được yêu cầu phân loại: chọn Recurring Budget nếu muốn ngân sách lặp lại hoặc chọn Expiring Budget nếu chỉ muốn áp dụng một lần.
- Tiếp theo là cấu hình Budgeting method: chọn Fixed nếu muốn ngân sách mỗi kỳ giống nhau hoặc chọn Planned nếu muốn đặt ngân sách khác nhau theo từng tháng.
- Nhập Budgeted amount theo mức chi phí mong muốn.
- Để có cái nhìn tổng quan, trong Budget scope, chọn All AWS services.
- Đảm bảo tính minh bạch bằng cách trong Aggregate costs by, chọn Unblended costs.
- Nhấn Next để chuyển sang bước cấu hình cảnh báo.
- Chọn Add an alert threshold.
- Nhập tỷ lệ cảnh báo, ví dụ 80% hoặc 100% và nhập email nhận cảnh báo.
- Kiểm tra lại toàn bộ cấu hình trước khi nhấn Create budget để hoàn tất. Cuối cùng là xác nhận Budget đã xuất hiện trong danh sách Budgets.

**Module 3 — Ràng buộc tài nguyên vật lý (Create Usage Budget)**
- Truy cập lại mục Budgets trong AWS Billing and Cost Management và nhấn Create budget.
- Chọn Customize nhưng trong Budget types, chọn Usage budget và nhấn Next để tiếp tục.
- Nhập tên cho Usage Budget.
- Trong phần Budget against, chọn Usage type groups. Đây là bước quan trọng để chọn loại usage cần theo dõi, ví dụ EC2: ELB - Running Hours.
- Tiến hành cấu hình Set budget amount với các chi tiết: chọn Period là Daily, Monthly, Quarterly hoặc Annually; chọn Budget renewal type là Recurring hoặc Expiring; chọn Budgeting method là Fixed hoặc Planned.
- Sau đó, nhập số giờ sử dụng tối đa muốn theo dõi và giữ cấu hình mặc định ở Budget scope nếu phù hợp với lab.
- Nhấn Next để cấu hình cảnh báo.
- Chọn Add an alert threshold.
- Nhập phần trăm cảnh báo so với ngân sách sử dụng và nhập email nhận thông báo.
- Review lại cấu hình và nhấn Create budget để hoàn tất.
- Theo dõi hệ thống bằng cách kiểm tra Budget health để xem mức sử dụng hiện tại so với giới hạn và mở Budget history để theo dõi xu hướng sử dụng.

**Module 4 & 5 — Mô phỏng quản trị doanh nghiệp (Create RI & Savings Plans Budgets)**
- Đối với RI: Truy cập AWS Billing and Cost Management > Chọn Budgets > Nhấn Create budget.
- Trong Budget setup, chọn Customize > Chọn Reservation budget > Nhấn Next.
- Nhập Budget name cho Reservation Budget.
- Thực hiện cấu hình Coverage threshold để theo dõi mức bao phủ của Reserved Instances.
- Cấu hình Budget scope theo hướng dẫn lab.
- Ở phần Alert setting, nhập email nhận cảnh báo. Review lại thông tin và nhấn Create budget.
- Kiểm tra Reservation Budget đã được tạo. Một bài học đúc kết quan trọng: ghi nhận rằng trong phạm vi lab không bắt buộc phải mua Reserved Instances vì có thể phát sinh chi phí hoặc yêu cầu cam kết thanh toán.
- Đối với Savings Plans: Truy cập AWS Billing and Cost Management > Chọn Budgets > Nhấn Create budget > Chọn Customize > Trong Budget types, chọn Savings Plans budget > Nhấn Next.
- Nhập Budget name cho Savings Plans Budget.
- Thực hiện cấu hình Utilization threshold để theo dõi mức sử dụng Savings Plans.
- Giữ Budget scope theo mặc định nếu phù hợp với lab.
- Ở phần Alert setting, nhập email nhận cảnh báo. Review lại toàn bộ cấu hình và nhấn Create budget để hoàn tất.
- Kiểm tra Budget vừa tạo trong danh sách. Tương tự RI, ghi nhận rằng Savings Plans thường liên quan đến cam kết sử dụng dài hạn nên trong môi trường học tập chỉ nên thao tác theo hướng dẫn hoặc xem demo.

**Module 6 — Kỷ luật dọn dẹp hệ thống (Clean Up Resources)**
- Truy cập AWS Billing and Cost Management và chọn Budgets ở menu bên trái.
- Kiểm tra danh sách các Budget đã tạo trong lab.
- Chọn Budget cần xóa và chọn Action.
- Nhấn Delete. Ở hộp thoại xác nhận, nhấn Delete để hoàn tất.
- Lặp lại thao tác với các Budget còn lại đã tạo trong quá trình thực hành.
- Kiểm tra lại danh sách Budgets sau khi xóa.
- Bước này củng cố kiến thức lý thuyết: ghi nhận rằng việc xóa Budget chỉ xóa cấu hình theo dõi và cảnh báo, không ảnh hưởng đến các tài nguyên AWS đang chạy.

---

### Đánh giá kết quả tuần 5:

Chuỗi thực hành tuần này đã giúp tôi nâng cao đáng kể nhận thức về FinOps:
- Hoàn thành việc tìm hiểu dịch vụ AWS Budgets trong quản lý chi phí AWS.
- Biết cách tạo ngân sách bằng template có sẵn để thiết lập cảnh báo nhanh.
- Tạo được Cost Budget để theo dõi chi phí sử dụng AWS theo tháng.
- Tạo được Usage Budget để theo dõi mức sử dụng tài nguyên AWS.
- Hiểu được sự khác nhau giữa Cost Budget và Usage Budget.
- Nắm được mục đích của Reservation Budget trong việc theo dõi Reserved Instances.
- Nắm được mục đích của Savings Plans Budget trong việc theo dõi Savings Plans.
- Biết cấu hình alert threshold và email notification cho Budget.
- Biết kiểm tra Budget health và Budget history để đánh giá tình trạng ngân sách.
- Biết cleanup các Budget đã tạo trong môi trường lab.
- Từ đó, nhận thức rõ hơn về tầm quan trọng của kiểm soát chi phí khi thực hành trên AWS.

---

### Khó khăn gặp phải trong quá trình phân tích hệ thống:

- **Phức tạp về giao diện:** Giao diện Billing and Cost Management có nhiều mục nên ban đầu dễ nhầm giữa Bills, Cost Explorer và Budgets. Sự rạch ròi giữa quá khứ (Explorer) và tương lai (Budgets) đòi hỏi tư duy phân loại tốt.
- **Sự mơ hồ giữa các khái niệm:** Cần phân biệt rõ Cost Budget và Usage Budget vì hai loại Budget này theo dõi hai nhóm thông tin khác nhau. 
- **Lỗi thao tác UX:** Khi cấu hình Usage Budget, cần chọn đúng Usage type group để theo dõi đúng loại tài nguyên. Với hàng ngàn service, chỉ một click sai sẽ khiến Budget trở nên vô nghĩa.
- **Giới hạn tài khoản:** Một số tài khoản AWS mới có thể chưa hiển thị đầy đủ các loại Budget ngoài Cost Budget.
- **Độ trễ dữ liệu (Data Latency):** Dữ liệu chi phí và usage trên AWS có thể cập nhật chậm nên sau khi tạo Budget chưa thể thấy ngay số liệu đầy đủ. Điều này thường gây ra hiệu ứng hoang mang tâm lý khi thiết lập hệ thống.
- **Tính trừu tượng của hệ thống cam kết:** Phần RI Budget và Savings Plans Budget dễ gây nhầm lẫn vì liên quan đến các hình thức cam kết sử dụng dài hạn.
- **Rủi ro vận hành (Alert Fatigue):** Nếu cấu hình nhiều alert hoặc nhập sai email, người dùng có thể không nhận được cảnh báo như mong muốn, hoặc ngược lại, bị spam email liên tục dẫn đến "lờn" cảnh báo.
- **Lỗ hổng kiến thức căn bản:** Cần chú ý rằng AWS Budgets chỉ cảnh báo, không tự động dừng dịch vụ khi vượt ngân sách. Việc hiểu sai điều này có thể dẫn đến hậu quả nghiêm trọng về mặt tài chính.

---

### Hướng khắc phục và Best Practices đúc kết được:

- **Chủ động học tập:** Đọc kỹ từng bước trong workshop trước khi thao tác trên AWS Console.
- **Hệ thống hóa bằng ghi chú:** Ghi chú lại mục đích của từng loại Budget để tránh nhầm lẫn:
  - Cost Budget dùng để theo dõi chi phí.
  - Usage Budget dùng để theo dõi mức sử dụng tài nguyên.
  - Reservation Budget dùng để theo dõi Reserved Instances.
  - Savings Plans Budget dùng để theo dõi Savings Plans.
- **Kiểm soát rủi ro thông tin:** Khi cấu hình cảnh báo, nên nhập đúng email và kiểm tra hộp thư để xác nhận nhận thông báo. 
- **Xây dựng chiến lược cảnh báo đa tầng:** Nên đặt nhiều mức cảnh báo như 50%, 80% và 100% để chủ động kiểm soát chi phí.
- **An toàn thực hành:** Tránh các thao tác tạo cam kết tài chính bừa bãi. Tuyệt đối không nên mua Reserved Instances hoặc Savings Plans trong tài khoản học tập nếu không có yêu cầu chính thức.
- **Kỷ luật vận hành hệ thống:** 
  - Sau khi hoàn thành lab, cần xóa các Budget thực hành để tránh nhận thông báo không cần thiết.
  - Kiểm tra lại Billing Dashboard sau mỗi buổi lab để phát hiện chi phí bất thường.
  - Kết hợp AWS Budgets với thói quen cleanup tài nguyên để hạn chế phát sinh chi phí ngoài ý muốn.

---

### Định hướng tối ưu cho tuần tiếp theo:

Hành trình FinOps không dừng lại ở việc đặt giới hạn (Budgets), mà sẽ mở rộng sang khía cạnh phân tích và dò tìm nâng cao. Các chuyên đề nghiên cứu sắp tới bao gồm:
- Tiếp tục tìm hiểu sâu hơn về AWS Billing and Cost Management.
- Nghiên cứu thêm AWS Cost Explorer để phân tích chi phí theo dịch vụ, thời gian và tài khoản.
- Tìm hiểu cách sử dụng AWS Free Tier Dashboard để theo dõi giới hạn miễn phí, bảo vệ ngân sách học tập tối đa.
- Tìm hiểu AWS Cost Anomaly Detection để phát hiện chi phí bất thường (ứng dụng Machine Learning vào dò tìm dữ liệu).
- Nghiên cứu thêm về AWS Organizations và cách quản lý chi phí cho nhiều tài khoản AWS (kiến trúc Multi-account).
- Thực hành xây dựng thói quen kiểm tra Billing Dashboard sau mỗi bài lab.
- Cuối cùng, luôn đảm bảo việc chuẩn bị ảnh minh chứng, ghi chú thao tác và nhận xét kết quả để hoàn thiện báo cáo tuần tiếp theo.