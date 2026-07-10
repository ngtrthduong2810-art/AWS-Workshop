---
title: "Worklog Tuần 7"
date: 2026-05-29
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Mục tiêu tuần 7: Xây dựng nền tảng Bảo mật và Hạ tầng mạng lõi

Bước sang tuần thứ 7, chúng ta chạm đến hai trụ cột quan trọng nhất quyết định sự an toàn và khả năng kết nối của mọi hệ thống trên Cloud: Bảo mật danh tính và Kiến trúc mạng cô lập. Mục tiêu của tuần này là chuyển đổi tư duy từ việc chỉ biết "khởi chạy tài nguyên" sang việc "bảo vệ và định tuyến" chúng một cách có hệ thống. Các mục tiêu trọng điểm bao gồm:

- **Làm chủ hệ thống phân quyền (IAM):** Tìm hiểu tổng quan về AWS Identity and Access Management (IAM) nhằm hiểu vai trò của IAM trong việc quản lý danh tính và phân quyền trên AWS. 
- **Thiết lập rào chắn xác thực:** Tìm hiểu cơ chế xác thực và bảo mật tài khoản với Multi-Factor Authentication (MFA) để bảo vệ tài khoản khỏi các nguy cơ xâm nhập.
- **Thực thi phân quyền cấp hạt (Granular Permissions):** Thực hành tạo và quản lý IAM User, Group, Role và Policy, đồng thời tìm hiểu các nguyên tắc bảo mật và phân quyền theo Principle of Least Privilege (Nguyên tắc đặc quyền tối thiểu).
- **Kiến tạo hạ tầng mạng độc lập (VPC):** Tìm hiểu tổng quan về Amazon Virtual Private Cloud (Amazon VPC) để hiểu kiến trúc mạng của Amazon VPC và các thành phần cơ bản cấu thành nên một trung tâm dữ liệu ảo.
- **Định tuyến và Phân vùng mạng:** Thực hành tạo và cấu hình VPC, Subnet, Route Table và Internet Gateway nhằm kiểm soát luồng giao thông mạng đi ra/vào hệ thống.
- **Thiết lập tường lửa đa lớp:** Thực hành cấu hình Security Group và Network ACL để bảo vệ các máy chủ ở cấp độ mạng, qua đó nâng cao kỹ năng quản lý bảo mật và hạ tầng mạng trên AWS.

---

### Các công việc cần triển khai trong tuần này:

| Thứ | Hạng mục công việc chuyên sâu | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 2 | - **Nghiên cứu nền tảng IAM:** Đọc tổng quan workshop AWS IAM. <br> - Đào sâu lý thuyết để tìm hiểu vai trò của IAM trong AWS. <br> - Bắt đầu chuẩn bị môi trường thực hành. | 15/06/2026 | 15/06/2026 | https://000009.awsstudygroup.com/ |
| 3 | - **Định danh và Phân quyền:** Tìm hiểu IAM User, Group, Role và Policy. <br> - Trực tiếp thực hành tạo User và Group để tổ chức nhân sự ảo. <br> - Cấp quyền bằng Managed Policy để tận dụng các bộ quy tắc chuẩn của AWS. | 16/06/2026 | 16/06/2026 | https://000009.awsstudygroup.com/ |
| 4 | - **Gia cố bảo mật tài khoản:** Tìm hiểu Multi-Factor Authentication (MFA). <br> - Trực tiếp cấu hình MFA cho tài khoản. <br> - Nghiên cứu các nguyên tắc bảo mật AWS để hình thành tư duy DevSecOps. | 17/06/2026 | 17/06/2026 | https://000009.awsstudygroup.com/ |
| 5 | - **Nghiên cứu nền tảng Mạng:** Đọc tổng quan workshop Amazon VPC. <br> - Phân tích lý thuyết và tìm hiểu kiến trúc mạng VPC. <br> - Làm quen với các thành phần mạng như IP, Subnet, Routing. | 18/06/2026 | 18/06/2026 | https://000010.awsstudygroup.com/ |
| 6 | - **Kiến tạo Mạng Ảo:** Tiến hành tạo Virtual Private Cloud (VPC). <br> - Phân vùng mạng bằng cách cấu hình Public và Private Subnet. <br> - Thiết lập Internet Gateway và Route Table để mở đường giao tiếp với Internet. | 19/06/2026 | 19/06/2026 | https://000010.awsstudygroup.com/ |
| 7 | - **Cấu hình Tường lửa:** Cấu hình Security Group và Network ACL. <br> - Thực hiện kiểm tra kết nối giữa các tài nguyên bằng các lệnh ping/ssh. <br> - Khắc phục lỗi và hoàn thiện cấu hình mạng. | 20/06/2026 | 20/06/2026 | https://000010.awsstudygroup.com/ |
| CN | - **Đánh giá và Dọn dẹp:** Kiểm tra các tài nguyên đã tạo. <br> - Thực hiện Cleanup Resources để tối ưu chi phí lab. <br> - Viết báo cáo và tổng kết kiến thức đã học trong tuần. | 21/06/2026 | 21/06/2026 | https://000009.awsstudygroup.com/ <br> https://000010.awsstudygroup.com/ |

---

### Kết quả đạt được Tuần 7: Đúc kết kiến thức chuyên sâu

#### 1. Kiến trúc Bảo mật (AWS IAM & Account Security)
Kiến thức cốt lõi đầu tiên tôi làm chủ là hiểu IAM là dịch vụ quản lý danh tính và quyền truy cập trên AWS. Tôi đã biết cách tạo và quản lý IAM User, Group, Role và Policy. Tư duy bảo mật của tôi được nâng cấp khi hiểu nguyên tắc phân quyền tối thiểu (Least Privilege), đảm bảo mỗi thực thể chỉ có đúng và đủ quyền để làm việc, không hơn không kém.

Bên cạnh đó, tôi đã có khả năng phân biệt AWS Managed Policy và Customer Managed Policy, hiểu cách quản lý thông tin xác thực và quyền truy cập. Để bảo vệ ranh giới ngoài cùng, tôi hiểu vai trò của Multi-Factor Authentication (MFA) và biết cách cấu hình MFA cho tài khoản AWS. Qua đó, tôi nắm vững và hiểu các nguyên tắc bảo mật tài khoản và thông tin xác thực, đặc biệt là biết cách bảo vệ tài khoản Root và IAM User.

#### 2. Kiến trúc Hạ tầng Mạng (Amazon VPC & Network Security)
Tôi đã hiểu kiến trúc và chức năng của Amazon VPC, đóng vai trò như một trung tâm dữ liệu thu nhỏ trên đám mây. Việc nắm được khái niệm CIDR Block, Subnet và địa chỉ IP giúp tôi quy hoạch không gian mạng mạch lạc. Hơn nữa, tôi đã hiểu vai trò của Internet Gateway và Route Table trong việc dẫn đường cho các gói tin, từ đó có thể phân biệt Public Subnet và Private Subnet một cách rạch ròi.

Về mặt bảo vệ luồng giao thông mạng, tôi hiểu chức năng của Security Group (hoạt động ở cấp độ Instance) và hiểu cơ chế hoạt động của Network ACL (hoạt động ở cấp độ Subnet). Tôi đã biết cách cấu hình các quy tắc Inbound và Outbound để kiểm soát chặt chẽ dữ liệu vào ra. Kết quả cuối cùng là tôi đã hiểu nguyên tắc xây dựng hệ thống mạng an toàn trên AWS.

---

### Trải nghiệm Thực hành: Phân tích các Module

**Module 1 — AWS IAM**
- Đăng nhập và truy cập dịch vụ IAM.
- Tiến hành tạo IAM User và Group, tổ chức người dùng vào các nhóm có chung chức năng.
- Gán quyền bằng Managed Policy thay vì cấp quyền trực tiếp cho từng cá nhân.
- Khởi tạo IAM Role để cấp quyền tạm thời cho các dịch vụ (ví dụ EC2) gọi API.
- Tăng cường bảo mật bằng cách cấu hình Multi-Factor Authentication (MFA) thông qua ứng dụng Authenticator.
- Thực hiện kiểm tra quyền truy cập để xác nhận chính sách hoạt động đúng.

**Module 2 — AWS Security**
- Dành thời gian tìm hiểu các nguyên tắc bảo mật trên AWS.
- Thiết lập và cấu hình phương thức xác thực an toàn.
- Nghiêm ngặt áp dụng nguyên tắc phân quyền tối thiểu trong mọi chính sách.
- Chủ động kiểm tra cấu hình bảo mật tài khoản thông qua IAM Security Status.

**Module 3 — Amazon VPC**
- Đọc tài liệu để tìm hiểu kiến trúc Amazon VPC.
- Trực tiếp khởi tạo Virtual Private Cloud với dải CIDR tùy chỉnh.
- Phân tách kiến trúc bằng cách tạo Public và Private Subnet.
- Mở luồng giao tiếp bằng cách cấu hình Internet Gateway và thiết lập Route Table.

**Module 4 — Network Security**
- Tạo và cấu hình Security Group để mở cổng 22 (SSH) và 80 (HTTP).
- Bổ sung lớp phòng thủ mạng lưới bằng cách thiết lập Network ACL.
- Khởi chạy máy ảo và kiểm tra kết nối mạng.
- Dùng các công cụ diagnostic để xác minh hoạt động của các thành phần mạng.

**Module 5 — Cleanup Resources**
- Đảm bảo không phát sinh phí ẩn bằng cách kiểm tra toàn bộ tài nguyên đã tạo.
- Thực hiện xóa các tài nguyên không còn sử dụng theo đúng thứ tự (xóa Instance -> xóa Subnet/IGW -> xóa VPC).
- Xác nhận hoàn tất quá trình dọn dẹp.

---

### Đánh giá mức độ hoàn thành Tuần 7:

- Đã hiểu vai trò của AWS IAM trong quản lý danh tính và phân quyền.
- Tạo và quản lý thành công IAM User, Group, Role và Policy.
- Cấu hình thành công Multi-Factor Authentication (MFA).
- Hiểu các nguyên tắc bảo mật tài khoản AWS.
- Tạo và cấu hình thành công Amazon VPC.
- Thiết lập Public Subnet, Private Subnet, Route Table và Internet Gateway tạo thành một hệ thống mạng khép kín.
- Cấu hình Security Group và Network ACL để bảo vệ hệ thống.
- Qua đó, nâng cao kỹ năng quản lý bảo mật và hạ tầng mạng trên nền tảng AWS.

---

### Những khó khăn và Rào cản kỹ thuật:

- **Khái niệm Danh tính:** Ban đầu rất khó phân biệt giữa IAM Role và IAM User trong một số trường hợp sử dụng.
- **Cơ chế Phân quyền:** Do có quá nhiều loại policy, tôi còn nhầm lẫn giữa Managed Policy và Inline Policy.
- **Tường lửa đa lớp:** Việc phân biệt Security Group và Network ACL còn chưa rõ ràng (một bên là stateful, một bên là stateless).
- **Quy hoạch mạng:** Mất thời gian để hiểu cách hoạt động của Route Table và CIDR Block vì đòi hỏi tính toán subnet mask phức tạp.
- **Troubleshooting:** Gặp một số lỗi kết nối do cấu hình mạng chưa chính xác (quên gắn Route Table vào Subnet hoặc chặn nhầm port ở NACL).

---

### Hướng khắc phục và Giải pháp:

- **Bổ sung lý thuyết:** Đọc kỹ tài liệu AWS Study Group và AWS Documentation để hệ thống hóa kiến thức.
- **Rèn luyện kỹ năng:** Thực hành nhiều lần việc tạo User, Group, Role và Policy để quen với giao diện và logic cấp quyền.
- **Trực quan hóa:** Tự tay vẽ sơ đồ kiến trúc VPC để dễ hình dung luồng kết nối, từ đó không bị sót các gateway.
- **Checklist kiểm tra:** Trước khi test mạng, luôn kiểm tra kỹ Route Table, Security Group và Network ACL trước khi kiểm thử.
- **Tuân thủ quy chuẩn:** Kiên quyết áp dụng nguyên tắc Least Privilege trong quá trình cấp quyền, dù việc cấp full quyền (Admin) có vẻ dễ dàng hơn để vượt qua lỗi ban đầu.

---

### Định hướng mở rộng cho tuần tiếp theo:

Sau khi xây dựng xong hạ tầng mạng và bảo mật qua giao diện Console, bước tiếp theo là tiến tới tự động hóa và thao tác chuyên nghiệp bằng Command Line.
- Tìm hiểu AWS Command Line Interface (AWS CLI).
- Tiến hành cài đặt và cấu hình AWS CLI trên máy tính cá nhân.
- Nâng cấp kỹ năng bằng cách thực hành quản lý tài nguyên AWS bằng dòng lệnh.
- Tích hợp và làm việc với Amazon S3, SNS, IAM, VPC và EC2 thông qua AWS CLI.
- Cuối cùng, luôn chuẩn bị hình ảnh minh chứng và hoàn thiện báo cáo thực hành tuần tiếp theo.