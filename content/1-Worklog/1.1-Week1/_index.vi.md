---
title: "Worklog Tuần 1"
date: 2026-04-17
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---

### Mục tiêu trọng tâm của Tuần 1: Khởi động tư duy Cloud-Native

Tuần đầu tiên là bước đệm quan trọng nhất để chuyển đổi tư duy từ hạ tầng máy chủ vật lý (On-premises) sang môi trường linh hoạt của Cloud. Mục tiêu không chỉ là biết dùng công cụ, mà là hiểu cốt lõi kiến trúc:
- Chủ động hòa nhập vào môi trường làm việc và kết nối với các thành viên thuộc dự án First Cloud Journey.
- Xây dựng nền tảng kiến thức vững chắc về Điện toán đám mây và khám phá hệ sinh thái dịch vụ đa dạng của AWS.
- Đi sâu tìm hiểu kiến trúc hạ tầng toàn cầu, làm chủ các công cụ quản trị và rèn luyện tư duy tối ưu hóa chi phí (FinOps) ngay từ ngày đầu.
- Thiết lập thành công tài khoản AWS Free Tier 2025 và chinh phục mốc $200 credit hỗ trợ để tạo hành trang tài chính an toàn cho các bài lab sau này.
- Thực thi chuẩn xác các bài lab cốt lõi xoay quanh việc thiết lập tài khoản, tăng cường bảo mật và giám sát ngân sách nhằm hình thành kỷ luật vận hành chuẩn mực.

---

### Nhật ký triển khai công việc chuyên sâu:

| Thứ | Hạng mục công việc chuyên sâu | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham chiếu |
| --- | --- | --- | --- | --- |
| 2 | - **Hội nhập văn hóa:** Giao lưu và làm quen với đội ngũ FCJ. <br> - Nghiên cứu kỹ lưỡng các quy định, nội quy vận hành tại nơi thực tập để đảm bảo quy trình làm việc chuyên nghiệp và liền mạch. | 20/04/2026 | 20/04/2026 | https://www.notion.so/Group-description-TP-HCM-347df829a730809a8f63d39505644917 |
| 3 | - **Nghiên cứu nền tảng:** Khám phá Module 01-01: Bản chất của Điện Toán Đám Mây. <br> - Khám phá Module 01-02: Vị thế và sự khác biệt của AWS so với các nhà cung cấp khác. <br> - Khám phá Module 01-03: Hoạch định lộ trình chinh phục Cloud. <br> - Khám phá Module 01-04: Giải mã Hạ Tầng Toàn Cầu AWS để hiểu cách thiết kế hệ thống có tính sẵn sàng cao. | 21/04/2026 | 21/04/2026 | https://cloudjourney.awsstudygroup.com/ |
| 4 | - **Công cụ và Bảo mật:** Nghiên cứu Module 01-05: Cẩm nang Công Cụ Quản Lý AWS. <br> - Nghiên cứu Module 01-06: Chiến lược Tối Ưu Chi Phí & Tương tác với AWS Support. <br> - Module 01-07: Đào sâu nghiên cứu và ứng dụng thực tiễn. <br> - **Triển khai Thực hành:** <br>&emsp;+ Lab01-01: Khởi tạo thành công tài khoản AWS. <br>&emsp;+ Lab01-02: Thiết lập lớp bảo vệ Virtual MFA. <br>&emsp;+ Lab01-03: Phân quyền qua việc tạo Admin group & user. <br>&emsp;+ Lab01-04: Thử nghiệm quy trình yêu cầu Support xác thực. | 22/04/2026 | 22/04/2026 | https://000001.awsstudygroup.com/ <br> https://000002.awsstudygroup.com/ |
| 5 | - **Thực thi Quản trị Ngân sách (FinOps):** <br>&emsp;+ Lab07-01: Triển khai Budget nhanh qua Template. <br>&emsp;+ Lab07-02: Cấu hình Cost Budget kèm ngưỡng cảnh báo. <br>&emsp;+ Lab07-03: Thiết lập Usage Budget để giám sát tài nguyên. <br>&emsp;+ Lab07-04: Theo dõi cam kết qua RI Budget. <br>&emsp;+ Lab07-05: Quản trị gói Savings Plans Budget. <br>&emsp;+ Lab07-06: Thực hiện dọn dẹp (clean up) toàn bộ Budgets sau khi kiểm thử. | 23/04/2026 | 23/04/2026 | https://000001.awsstudygroup.com/ |
| 6 | - **Chinh phục thử thách:** Hoàn thành 5 thử thách để mở khóa $200 credit: <br>&emsp;+ Vận hành EC2 Instance (+$20). <br>&emsp;+ Trải nghiệm AI với Amazon Bedrock (+$20). <br>&emsp;+ Cấu hình cảnh báo AWS Budgets (+$20). <br>&emsp;+ Khởi tạo Lambda Web App (+$20). <br>&emsp;+ Triển khai RDS Database (+$20). <br> - Mở rộng kiến thức về chuẩn mực kiến trúc: AWS Well-Architected Framework. | 24/04/2026 | 24/04/2026 | https://000001.awsstudygroup.com/ <br> https://docs.aws.amazon.com/wellarchitected/ |

---

### Cột mốc và Thành quả Tuần 1: Đúc kết kiến thức chuyên sâu

#### Hành trang Kiến thức Cốt lõi

**1. Bản chất của Điện Toán Đám Mây**
- Nắm bắt sâu sắc triết lý của Cloud: thanh toán linh hoạt với mô hình dùng đến đâu trả tiền đến đó (pay-as-you-go) và cấp phát tức thời theo hình thức cung cấp tài nguyên theo nhu cầu (on-demand).
- Phân định rạch ròi cấp độ quản lý của các mô hình dịch vụ: IaaS, PaaS và SaaS.
- Nhận diện sự khác biệt về quyền kiểm soát và bảo mật giữa các phương thức triển khai: Public, Private và Hybrid Cloud.

**2. Vị thế độc tôn và Hệ sinh thái AWS**
- Nhận thức được quy mô khổng lồ của nền tảng AWS với hệ sinh thái vượt mốc 200 dịch vụ.
- Phân tích các ưu điểm cốt lõi làm nên tên tuổi AWS: bảo mật nghiêm ngặt, tính sẵn sàng cao, độ đàn hồi linh hoạt và bài toán chi phí.
- Hệ thống hóa các dịch vụ thành các nhóm trọng điểm để dễ dàng tra cứu kiến trúc:
  - Năng lực tính toán (Compute): EC2, Lambda.
  - Không gian lưu trữ (Storage): S3, EBS.
  - Mạng lưới (Networking): VPC, Security Group.
  - Dữ liệu (Database): RDS, Aurora.
  - Trí tuệ nhân tạo (AI/ML): Amazon Bedrock.

**3. Hoạch định lộ trình và Khai thác Free Tier**
- Phác thảo chặng đường phát triển kỹ năng AWS từ newbie đến chuyên gia.
- Bóc tách chi tiết chính sách ưu đãi AWS Free Tier 2025:
  - Bỏ túi ngay $100 credit sau cú click tạo tài khoản thành công.
  - Biết cách săn thêm $100 credit qua 5 bài lab thực tế.
  - Đánh giá sự được mất giữa Free Plan (an toàn trong 6 tháng) và Paid Plan (mở khóa toàn bộ rào cản dịch vụ) để đưa ra quyết định đăng ký phù hợp.

**4. Giải mã Hạ Tầng Toàn Cầu (Global Infrastructure)**
- Trực quan hóa mạng lưới vật lý của AWS thông qua các Region và Availability Zone (AZ) trải dài khắp thế giới.
- Củng cố định nghĩa về Region, AZ và các điểm chạm Edge Location trong mạng CDN.
- Hình thành tư duy chọn Region chiến lược dựa trên các yếu tố: độ trễ mạng, ngân sách và rào cản pháp lý (data compliance).

**5. Cẩm nang Công Cụ Quản Lý & Tối ưu Chi phí**
- Làm quen với thao tác trực quan qua giao diện web AWS Management Console.
- Tiếp cận sức mạnh của khả năng tự động hóa thông qua AWS CLI và lập trình qua SDK, cùng sự tiện dụng của môi trường trình duyệt AWS CloudShell.
- Khám phá bộ 3 công cụ gác cổng chi phí: AWS Budgets, Cost Explorer và báo cáo Cost & Usage Report.
- Học cách mua sắm thông minh thông qua các cam kết dài hạn với Reserved Instances, Savings Plans và Spot Instances.
- Phân loại các cấp độ Support (Basic, Developer, Business, Enterprise) và thực hành mở một ticket hỗ trợ đúng chuẩn kỹ thuật.

**6. Nghiên cứu chuyên sâu — Khung Well-Architected**
- Khắc sâu 6 trụ cột thiết kế hệ thống hoàn hảo (Best Practices): Vận hành xuất sắc, Bảo mật, Đáng tin cậy, Hiệu suất, Tối ưu chi phí và Tính bền vững. Đây chính là kim chỉ nam cho mọi bản vẽ kiến trúc Cloud.

---

#### Dấu ấn Thực hành: Từ Lý thuyết đến Vận hành

**Module Khởi tạo và Bảo mật Cơ sở:**
- **Lab01-01:** Tự tay truy cập [aws.amazon.com/free](https://aws.amazon.com/free) để đăng ký tài khoản. Tôi đã quyết đoán chọn **Paid Plan** nhằm đảm bảo quá trình thực hành không bị giới hạn. Ngay sau đó, tôi ghi nhận thành công khoản $100 credit được nạp tự động vào hệ thống.
- **Lab01-02:** Để bảo vệ quyền kiểm soát tối cao, tôi thiết lập ngay khiên bảo vệ MFA cho tài khoản root thông qua ứng dụng Authenticator.
- **Lab01-03:** Tuân thủ nguyên tắc đặc quyền tối thiểu, tôi xây dựng nhóm `AdminGroup` và cấp cho nhóm này quyền lực tối cao `AdministratorAccess`. Sau đó, tôi khởi tạo IAM User riêng biệt và đưa vào nhóm để sử dụng cho công việc hàng ngày thay vì dùng tài khoản Root.
- **Lab01-04:** Giả lập tình huống thực tế và tiến hành mở case yêu cầu xác minh tài khoản thành công để làm quen với quy trình vận hành Support.

**Module Quản trị Tài chính (AWS Budgets):**
- **Lab07-01 đến 07-06:** Thực hành toàn diện hệ thống quản lý chi phí. Bắt đầu bằng việc khởi tạo chớp nhoáng một Budget dựa trên Template, sau đó tự tay cấu hình Cost Budget với cơ chế báo động qua email khi vượt ngưỡng. Tiếp tục vận hành Usage Budget để đong đếm tài nguyên (giờ tính toán, dung lượng GB), và triển khai các Budget nâng cao cho RI và Savings Plans. Cuối cùng, tôi đảm bảo nguyên tắc sạch sẽ (clean up) bằng việc xóa toàn bộ Budget sau khi test xong.

**Chiến dịch Mở khóa $200 Credit (5 Thử thách):**
- **Thử thách 1 (EC2):** Khởi chạy thành công một EC2 instance mang tên `Test Instance`, với các thao tác chuẩn xác từ khâu chọn AMI đến cấu hình Security Group. Tôi tự tạo và tải về chìa khóa `first-kp` (định dạng RSA, .pem) để truy cập từ xa. Quan trọng nhất, tôi đã dọn dẹp tài nguyên (Terminate) triệt để ngay sau khi hoàn tất và đánh dấu hoàn thành mốc đầu tiên.
- **Thử thách 2 (AI/ML):** Truy cập trung tâm điều khiển Bedrock và gọi thành công model **Claude 3 Haiku**. Tôi đã bơm dữ liệu use case và test thử một prompt để xem phản hồi, qua đó cán mốc thử thách số hai.
- **Thử thách 3 (FinOps):** Giăng lưới bảo vệ bằng một Cost budget kết nối thẳng tới email cá nhân.
- **Thử thách 4 (Serverless):** Triển khai siêu tốc một Lambda function (`http-function-url-tutorial`) từ kho blueprint có sẵn, và tuân thủ kỷ luật dọn dẹp function không thương tiếc ngay sau khi test.
- **Thử thách 5 (Database):** Dựng thành công một cụm Aurora (tương thích PostgreSQL) bằng tính năng Easy Create. Sau khi hệ thống chạy ổn định, tôi xóa trắng DB instance và cluster để cắt giảm chi phí phát sinh.

---

#### Góc nhìn Khó khăn & Giải pháp Vận hành

**Những chướng ngại vật:**
- Đứng hình mất một lúc vì bối rối giữa lựa chọn Free Plan hay Paid Plan ở khâu đăng ký do lo ngại phát sinh chi phí ngoài ý muốn.
- Bị hệ thống chặn quyền (authorization error) khi cố gắng gọi model Claude 3 Haiku trên Amazon Bedrock.
- Khá ngợp và lóng ngóng trước giao diện đồ sộ của AWS Console trong những lần click đầu tiên.
- Mơ hồ trong việc phân định lúc nào dùng Budget nào (Cost, Usage, RI, Savings Plans) trong các tình huống thực tế.

**Chiến thuật tháo gỡ:**
- Dừng lại đọc thật kỹ bảng so sánh tính năng giữa hai Plan trước khi ra quyết định để đảm bảo lộ trình học tập không bị cản trở.
- Đối mặt với lỗi quyền truy cập AI, tôi chủ động tạo một Support case (Mục Account & billing > Bedrock Allowlisting) và kiên nhẫn chờ AWS phê duyệt sau 24h.
- Lấy cần cù bù bỡ ngỡ: click và thao tác đi lại nhiều lần trên giao diện để não bộ ghi nhớ vị trí các dịch vụ.
- Lật lại tài liệu lý thuyết, đối chiếu từng loại Budget và tự mình làm lại từng bài lab một cách chậm rãi để hiểu sâu bản chất dòng tiền trên Cloud.

---

#### Đúc kết Kinh nghiệm Tuần 1

- Cảm nhận rõ ràng sức mạnh của nền tảng Cloud và hiểu tại sao AWS lại đang thống trị cuộc chơi công nghệ.
- Hình thành ý thức bảo mật tối cao: Phải **bật MFA** ngay lập tức và tuyệt đối cất kỹ tài khoản Root, chỉ dùng IAM User cho các tác vụ hàng ngày.
- Khắc cốt ghi tâm bài học tài chính: **Cài đặt Budget là việc phải làm đầu tiên** để không bị sốc khi nhận hóa đơn.
- Luyện thành phản xạ **"dọn dẹp sạch sẽ"** tài nguyên (như terminate máy ảo, xóa database) ngay khi thực hành xong.
- Nhận thức được AWS Well-Architected Framework chính là kim chỉ nam không thể thiếu cho bất kỳ bản vẽ thiết kế hệ thống nào sau này.