---
title: "Worklog Tuần 3"
date: 2026-04-28
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Mục tiêu tuần 3: Làm chủ năng lực điện toán và vận hành máy chủ

Sau khi đã xây dựng thành công hạ tầng mạng ở tuần trước, tuần thứ 3 là bước tiến quan trọng vào việc triển khai và vận hành các khối tính toán (Compute) trên đám mây. Mục tiêu cốt lõi không chỉ là biết cách bật/tắt một máy chủ, mà là hiểu sâu sắc về vòng đời của nó, cách tối ưu hóa, và bảo mật ở cấp độ Instance. Các mục tiêu chuyên sâu bao gồm:

- **Khám phá năng lực tính toán:** Tìm hiểu tổng quan về Amazon EC2 và vai trò của EC2 trong hạ tầng Cloud như một động cơ xử lý cốt lõi của mọi ứng dụng.
- **Xây dựng rào chắn bảo mật:** Thực hành tạo VPC, Security Group cho Linux và Windows Instance nhằm thiết lập các quy tắc tường lửa nghiêm ngặt cấp độ máy chủ.
- **Vận hành hệ thống:** Trực tiếp khởi tạo, kết nối và quản lý EC2 Instance trên AWS với cả hai nền tảng hệ điều hành phổ biến nhất.
- **Làm chủ quản trị nâng cao:** Làm quen với các thao tác cơ bản: đổi Instance Type, tạo Snapshot, tạo AMI, khôi phục truy cập để đảm bảo tính liên tục của doanh nghiệp (Business Continuity).
- **Thực chiến triển khai phần mềm:** Vận dụng môi trường vừa tạo để triển khai thử ứng dụng AWS User Management trên Linux và Windows Server, đánh giá sự khác biệt giữa hai hệ sinh thái.
- **Thiết lập kỷ luật vận hành (Governance):** Thực hành quản trị chi phí và quyền sử dụng EC2 bằng IAM Policy để ngăn chặn việc lạm dụng tài nguyên.
- **Tối ưu ngân sách:** Duy trì thói quen dọn dẹp tài nguyên sau khi hoàn thành lab để tránh phát sinh chi phí.

---

### Các công việc cần triển khai trong tuần này:

| Thứ | Hạng mục công việc chuyên sâu | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 2 | - **Nghiên cứu nền tảng:** Đọc phần Introduction từ Amazon EC2. <br> - Nắm tổng quan workshop và kiến trúc thực hành. <br> - Đảm bảo sẵn sàng bằng cách chuẩn bị tài khoản AWS, Region, Key Pair và môi trường kết nối. | 04/05/2026 | 04/05/2026 | https://000004.awsstudygroup.com/ |
| 3 | - **Kiến tạo Mạng & Bảo mật:** Module 2.1: Create a Linux VPC. <br> - Module 2.2: Create VPC for Windows Instance. <br> - Module 2.3: Create Security Group for Linux Instance. <br> - Module 2.4: Create Security Group for Windows Instance. | 05/05/2026 | 05/05/2026 | https://000004.awsstudygroup.com/ |
| 4 | - **Triển khai Windows Server:** Module 3.1: Launch Microsoft Windows Server 2022 Instance. <br> - Module 3.2: Connect from Computer to Windows Instance. <br> - Thao tác kiểm tra Remote Desktop và key pair đăng nhập Windows. | 06/05/2026 | 06/05/2026 | https://000004.awsstudygroup.com/ |
| 5 | - **Triển khai Linux Server:** Module 4.1: Launch Amazon Linux Instance. <br> - Module 4.2: Connect to Amazon Linux Instance. <br> - Tiến hành thực hành SSH vào Linux Instance bằng key pair. | 07/05/2026 | 07/05/2026 | https://000004.awsstudygroup.com/ |
| 6 | - **Quản trị Vòng đời EC2:** Module 5.1: Modify EC2 Instance Type. <br> - Module 5.2: Create and Manage EBS Snapshots. <br> - Khai thác sức mạnh AMI: Module 5.3: Create Custom AMI và Module 5.4: Launch Instance from Custom AMI. <br> - Xử lý sự cố: Module 5.5 - 5.7: Recover access và Remote Desktop Ubuntu. | 08/05/2026 | 08/05/2026 | https://000004.awsstudygroup.com/ |
| 7 | - **Triển khai Ứng dụng (Linux):** Module 6: Deploy AWS User Management Application on Amazon Linux. <br> - Xây dựng môi trường: cài LAMP Server, cấu hình database, phpMyAdmin, Node.js và deploy app. | 09/05/2026 | 09/05/2026 | https://000004.awsstudygroup.com/ |
| CN | - **Triển khai Ứng dụng (Windows) & Quản trị:** Module 7: Deploy Node.js Application on Windows EC2. <br> - Thiết lập rào cản: Module 8: Cost & Usage Governance with IAM. <br> - Kỷ luật tài chính: Module 9: Clean up resources. | 10/05/2026 | 10/05/2026 | https://000004.awsstudygroup.com/ |

---

### Kết quả đạt được Tuần 3: Đúc kết kiến thức chuyên sâu

#### 1. Kiến trúc Điện toán Đám mây (Amazon EC2)
Nền tảng kiến thức quan trọng nhất tôi nắm được là hiểu Amazon EC2 là dịch vụ cung cấp máy chủ ảo trên AWS. Nó không chỉ là một cái máy tính, mà EC2 cho phép tạo, cấu hình, kết nối và quản lý server theo nhu cầu với khả năng mở rộng không giới hạn. Sự linh hoạt của EC2 nằm ở việc có thể chạy nhiều hệ điều hành khác nhau như Amazon Linux, Ubuntu và Windows Server. Tôi nhận thấy EC2 thường được dùng để triển khai web server, backend, database thử nghiệm, ứng dụng nội bộ hoặc môi trường lab.

Quyết định sức mạnh của EC2 là Instance Type. Tôi đã hiểu rằng Instance Type quyết định CPU, RAM, network và khả năng xử lý của máy chủ. Khác với máy chủ vật lý, trên Cloud ta có thể stop instance rồi thay đổi Instance Type khi cần nâng hoặc giảm cấu hình (Scale Up/Down) chỉ trong vài phút. Do đó, việc chọn Instance Type cần dựa trên nhu cầu thực tế và chi phí.

#### 2. Tường lửa cấp độ máy chủ (Security Group) và Bảo mật kết nối
Dù máy chủ nằm trong VPC, nó vẫn cần lớp bảo vệ trực tiếp. Tôi đã hiểu VPC là mạng riêng ảo dùng để cô lập tài nguyên trên AWS và biết cách tạo VPC riêng cho Linux Instance và Windows Instance. Quan trọng hơn, tôi hiểu Security Group hoạt động như firewall cấp instance (Stateful firewall).

Việc kiểm soát truy cập yêu cầu sự chính xác cao. Tôi đã biết mở port phù hợp cho từng giao thức:
- **Quản trị từ xa:** SSH: `22` cho Linux và RDP: `3389` cho Windows.
- **Truy cập ứng dụng web:** HTTP: `80` cho web server và HTTPS: `443` cho web bảo mật.

Về mặt xác thực danh tính, Key Pair dùng để xác thực khi truy cập EC2. Cơ chế hoạt động khác nhau theo HĐH: với Linux, sử dụng file `.pem` để SSH; trong khi đó với Windows, sử dụng key pair để decrypt password rồi kết nối bằng Remote Desktop. Bài học đắt giá rút ra là nếu mất key pair, cần dùng phương án khôi phục như Systems Manager hoặc gắn volume sang instance khác để cứu dữ liệu.

#### 3. Sao lưu, Phục hồi và Đóng gói Môi trường (Snapshot & AMI)
Trong môi trường production, dữ liệu là sinh mệnh. Tôi đã thấu hiểu cơ chế EBS Snapshot dùng để sao lưu volume theo định dạng point-in-time. Để triển khai nhanh hàng loạt máy chủ giống hệt nhau, Custom AMI dùng để tạo image từ một instance đã cấu hình sẵn. Nhờ đó, ta có thể launch instance mới từ AMI để tái sử dụng môi trường đã cài đặt mà không cần cấu hình lại từ đầu (Golden Image).

#### 4. Quản trị Tuân thủ và Chi phí (Governance)
Việc cấp quyền tạo máy chủ bừa bãi sẽ dẫn đến thảm họa tài chính. Tôi đã biết dùng IAM Policy để giới hạn quyền sử dụng dịch vụ. Cụ thể, tôi có thể hạn chế tạo EC2 theo Region, Instance Family hoặc Instance Type (chỉ cho phép tạo t3.micro để học tập). Thậm chí, tôi có thể kiểm soát quyền xóa tài nguyên theo IP hoặc thời gian để ngăn chặn sự phá hoại. Qua đó, tôi hiểu tầm quan trọng của governance để tránh lạm dụng tài nguyên và phát sinh chi phí.

---

### Trải nghiệm Thực hành: Phân tích các Module

**Module 2 — Chuẩn bị Hạ tầng (Preparation)**
- Thiết kế mạng lưới bằng cách tạo VPC cho Linux Instance và tạo VPC cho Windows Instance.
- Quản lý rủi ro bằng cách tạo Security Group cho Linux: thiết lập rule cho phép SSH từ IP cá nhân (chặn hoàn toàn IP lạ) và cho phép HTTP nếu cần chạy web server.
- Tương tự, tạo Security Group cho Windows: cấu hình cho phép RDP từ IP cá nhân và tuân thủ nguyên tắc bảo mật là không mở `0.0.0.0/0` nếu không cần thiết.

**Module 3 & 4 — Khởi chạy Máy chủ đa nền tảng**
- **Windows:** Bắt đầu bằng việc chọn AMI Microsoft Windows Server 2022 và chọn Instance Type phù hợp với Free Tier hoặc lab. Tôi gán Key Pair để có thể lấy password và cấu hình Security Group cho phép RDP. Sau khi khởi tạo Windows EC2 Instance, tôi thao tác decrypt password bằng file key pair và kết nối vào Windows Instance bằng Remote Desktop.
- **Linux:** Quy trình tương tự nhưng tối ưu hơn. Chọn AMI Amazon Linux, chọn Instance Type phù hợp, gán Key Pair và cấu hình Security Group cho phép SSH. Sau khi khởi tạo Linux EC2 Instance, tôi dùng lệnh kết nối SSH vào instance bằng terminal.

**Module 5 — Quản trị EC2 Nâng cao (Amazon EC2 Basic)**
- Thực hành linh hoạt phần cứng bằng cách thay đổi Instance Type.
- Đảm bảo an toàn dữ liệu qua việc tạo và quản lý EBS Snapshot.
- Đóng gói ứng dụng bằng cách tạo Custom AMI từ EC2 Instance đã cấu hình và launch EC2 Instance mới từ Custom AMI thành công.
- Rèn luyện kỹ năng gỡ lỗi: tìm hiểu cách khôi phục truy cập Windows Instance và tìm hiểu cách khôi phục truy cập Linux Instance. Đồng thời, thử nghiệm thực hành Remote Desktop vào EC2 Ubuntu với giao diện GUI.

**Module 6 & 7 — Triển khai Ứng dụng Thực chiến (Deployment)**
- **Trên Linux:** Tôi tự tay cài đặt LAMP Web Server, sau đó kiểm tra Apache/PHP hoạt động mượt mà. Tiếp tục cấu hình database server, cài đặt phpMyAdmin, và cài Node.js trên Amazon Linux. Cuối cùng, tôi deploy ứng dụng AWS User Management và kiểm tra chức năng CRUD cơ bản của ứng dụng.
- **Trên Windows:** Thử nghiệm hệ sinh thái khác bằng cách cài XAMPP trên Windows Instance và cài Node.js trên Windows Instance. Tôi tiến hành deploy AWS User Management Application trên Windows Server và kiểm tra ứng dụng qua trình duyệt để đối chiếu hiệu năng.

**Module 8 & 9 — Quản trị rủi ro và Dọn dẹp (Governance & Clean up)**
- Trực tiếp viết IAM JSON để tạo IAM Policy giới hạn sử dụng dịch vụ theo Region và tạo Policy giới hạn EC2 theo Instance Family cùng với tạo Policy giới hạn EC2 theo Instance Type. Tôi cũng tạo Policy quản lý loại EBS Volume được phép dùng. Nhằm chống xóa nhầm tài nguyên, tôi tạo Policy giới hạn quyền xóa tài nguyên theo IP công ty và tạo Policy giới hạn quyền xóa tài nguyên theo thời gian.
- Ở bước kết thúc, tôi terminate các EC2 Instance không còn sử dụng, xóa EBS Volume không cần thiết, xóa Snapshot nếu không dùng nữa và xóa AMI đã tạo trong lab. Để hoàn tất, tôi xóa Security Group, VPC hoặc tài nguyên phụ nếu không còn cần và cẩn thận kiểm tra Billing Dashboard sau khi dọn dẹp.

---

### Những khó khăn và Rào cản kỹ thuật:

- **Kiến trúc mạng chằng chịt:** Đối với người mới, ban đầu dễ nhầm giữa VPC, Subnet và Security Group khi phải thiết kế kiến trúc cô lập.
- **Bảo mật xác thực:** Thao tác phức tạp khi kết nối Windows Instance, cần decrypt password bằng đúng key pair. Trong khi đó, khi SSH vào Linux, dễ lỗi do sai permission file `.pem`.
- **Luồng dữ liệu (Traffic Flow):** Nếu mở sai port hoặc sai source IP trong Security Group thì không thể kết nối (Time out error).
- **Rủi ro tài chính:** Một số tài nguyên như EBS Snapshot, AMI, Elastic IP có thể phát sinh phí nếu quên xóa, do chúng hoạt động ngầm dù máy chủ đã bị tắt.
- **Môi trường lập trình:** Khi deploy app, có thể gặp lỗi package, firewall, port hoặc database connection, đòi hỏi kỹ năng gỡ lỗi hệ thống (system troubleshooting).

---

### Hướng khắc phục và Giải pháp (Best Practices):

- **Tư duy thiết kế (Design Thinking):** Luôn lấy giấy bút kiểm tra lại kiến trúc mạng trước khi launch instance để đảm bảo luồng routing chính xác.
- **Tiêu chuẩn đặt tên (Naming Convention):** Tránh "lạc trôi" tài nguyên bằng cách đặt tên tài nguyên rõ ràng theo format (ví dụ: `fcj-linux-vpc`, `fcj-windows-vpc`, `fcj-linux-sg`, `fcj-windows-sg`).
- **Bảo mật Zero-Trust:** Kiên quyết chỉ mở SSH/RDP theo IP cá nhân, hạn chế mở toàn bộ Internet (0.0.0.0/0).
- **Tuân thủ OS Security:** Với Linux, chạy lệnh phân quyền key pair trước khi SSH. Lệnh bắt buộc là: `chmod 400 first-kp.pem` để khóa quyền đọc ghi của các user khác.

---

### Định hướng mở rộng cho tuần tiếp theo:

Hành trình chinh phục Cloud sẽ bước sang giai đoạn tối ưu chi phí và tự động hóa cảnh báo.
- Tiếp cận hệ thống quản trị ngân sách AWS Budgets để thiết lập các rào chắn tài chính chuyên sâu.
- Học cách phân tách Cost Budget và Usage Budget.
- Khám phá Amazon CloudWatch để thiết lập hệ thống cảnh báo (Alarms) dựa trên hiệu suất tiêu thụ của máy chủ EC2.
- Chuẩn bị nền tảng để xây dựng CloudWatch Dashboard, trực quan hóa sức khỏe của toàn bộ hạ tầng đã xây dựng trong 3 tuần qua.