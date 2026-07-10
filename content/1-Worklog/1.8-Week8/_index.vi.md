---
title: "Worklog Tuần 8"
date: 2026-06-04
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Mục tiêu tuần 8: Chuyển dịch tư duy từ ClickOps sang ScriptOps

Bước sang tuần thứ 8, trọng tâm học tập chuyển từ việc thao tác thủ công trên giao diện web (AWS Management Console) sang việc điều khiển hạ tầng bằng mã lệnh. Đối với một kỹ sư phần mềm, làm chủ dòng lệnh là bước đệm bắt buộc để tiến tới tự động hóa CI/CD. Các mục tiêu chuyên sâu bao gồm:

- **Khám phá sức mạnh dòng lệnh:** Tìm hiểu tổng quan về AWS Command Line Interface (AWS CLI) và hiểu vai trò của AWS CLI trong việc quản lý tài nguyên AWS một cách nhanh chóng, nhất quán.
- **Thiết lập môi trường chuẩn:** Cài đặt và cấu hình AWS CLI trên máy tính cá nhân, đảm bảo kết nối bảo mật đến Cloud.
- **Kiểm soát hạ tầng qua Terminal:** Thực hành kiểm tra và quản lý tài nguyên bằng AWS CLI, thay thế hoàn toàn các thao tác click chuột truyền thống.
- **Tương tác đa dịch vụ:**
  - Thực hành làm việc với Amazon S3 thông qua AWS CLI để quản lý lưu trữ đối tượng.
  - Tìm hiểu và sử dụng Amazon SNS bằng AWS CLI để vận hành hệ thống tin nhắn pub/sub.
  - Thực hành quản lý IAM bằng AWS CLI để phân quyền bảo mật.
  - Tìm hiểu cách quản lý Amazon VPC bằng AWS CLI để truy vấn kiến trúc mạng.
- **Khởi tạo tài nguyên linh hoạt:** Khởi tạo và quản lý Amazon EC2 bằng AWS CLI.
- **Kỷ luật dọn dẹp:** Thực hiện dọn dẹp tài nguyên sau khi hoàn thành bài thực hành bằng chính các câu lệnh CLI để tránh phát sinh chi phí.

---

### Các công việc cần triển khai trong tuần này:

| Thứ | Hạng mục công việc chuyên sâu | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 2 | - **Nghiên cứu nền tảng:** Đọc tổng quan workshop AWS CLI. <br> - Đánh giá và tìm hiểu vai trò của AWS CLI trong quy trình tự động hóa. <br> - Chuẩn bị môi trường thực hành trên hệ điều hành cục bộ. | 22/06/2026 | 22/06/2026 | https://000011.awsstudygroup.com/1-introduction/ |
| 3 | - **Thiết lập xác thực:** Cài đặt AWS CLI. <br> - Cấu hình Access Key và Region thông qua `aws configure`. <br> - Chạy các lệnh ping API để kiểm tra kết nối AWS CLI. | 23/06/2026 | 23/06/2026 | https://000011.awsstudygroup.com/2-prerequiste/ <br> https://000011.awsstudygroup.com/3-installation/ |
| 4 | - **Khám phá tài nguyên:** Dùng lệnh để kiểm tra thông tin tài nguyên AWS hiện có. <br> - Thực hành các lệnh AWS CLI cơ bản để làm quen với cấu trúc `aws <command> <subcommand> [options]`. | 24/06/2026 | 24/06/2026 | https://000011.awsstudygroup.com/4-check-resource/ |
| 5 | - **Quản trị Lưu trữ (S3):** Thực hành quản lý Amazon S3 bằng AWS CLI. <br> - Tạo Bucket mới bằng dòng lệnh. <br> - Chạy lệnh đồng bộ để Upload và Download dữ liệu. | 25/06/2026 | 25/06/2026 | https://000011.awsstudygroup.com/5-cli-with-s3/ |
| 6 | - **Quản trị Thông báo (SNS):** Thực hành Amazon SNS bằng AWS CLI. <br> - Khởi tạo hạ tầng bằng cách tạo Topic. <br> - Thao tác Gửi và kiểm tra Notification hoàn toàn qua terminal. | 26/06/2026 | 26/06/2026 | https://000011.awsstudygroup.com/6-cli-with-sns/ |
| 7 | - **Điều khiển Hạ tầng Lõi:** Quản lý IAM bằng AWS CLI. <br> - Làm việc với Amazon VPC để xuất thông tin mạng. <br> - Trực tiếp khởi tạo EC2 bằng AWS CLI thông qua việc truyền tham số AMI và KeyPair. | 27/06/2026 | 27/06/2026 | https://000011.awsstudygroup.com/7-cli-with-iam/ <br> https://000011.awsstudygroup.com/8-cli-with-vpc/ <br> https://000011.awsstudygroup.com/9-create-ec2/ |
| CN | - **Đánh giá và Dọn dẹp:** Kiểm tra các tài nguyên đã tạo. <br> - Thực hiện Cleanup Resources qua các lệnh delete/terminate. <br> - Tổng kết kiến thức đã học để củng cố kỹ năng Scripting. | 28/06/2026 | 28/06/2026 | https://000011.awsstudygroup.com/11-clean-up/ |

---

### Kết quả đạt được Tuần 8: Đúc kết kiến thức chuyên sâu

#### 1. Tư duy Tự động hóa với AWS CLI
Tôi đã hiểu AWS CLI là công cụ dòng lệnh giúp quản lý và tự động hóa các dịch vụ AWS. Sự khác biệt lớn nhất là tôi đã hiểu lợi ích của việc sử dụng CLI thay cho AWS Management Console trong nhiều trường hợp (như triển khai hàng loạt, lặp lại các tác vụ nhàm chán hoặc tích hợp vào bash script). Để giao tiếp với AWS, tôi biết cách cấu hình thông tin xác thực để kết nối đến tài khoản AWS.

Quá trình này bắt đầu bằng việc cài đặt AWS CLI trên hệ điều hành. Điểm mấu chốt là phải thiết lập một hồ sơ bảo mật bằng cách cấu hình Access Key, Secret Access Key, Region và Output Format (thường là JSON để dễ phân tích). Cuối cùng, tôi biết kiểm tra kết nối tới tài khoản AWS bằng các lệnh CLI như `aws sts get-caller-identity`.

#### 2. Thao tác Lưu trữ và Truyền thông (S3 & SNS)
Với lưu trữ, tôi đã biết tạo và quản lý S3 Bucket trực tiếp từ terminal. Các thao tác Upload, Download và liệt kê các đối tượng trong Bucket diễn ra nhanh chóng thông qua nhóm lệnh `aws s3`. Kết thúc vòng đời dữ liệu, tôi biết cách xóa dữ liệu và Bucket bằng AWS CLI.

Đối với hệ thống nhắn tin, tôi học được cách tạo SNS Topic. Sau đó, tôi thiết lập thiết bị nhận bằng cách đăng ký Subscription và chủ động gửi Notification thông qua AWS CLI.

#### 3. Quản trị Hạ tầng cốt lõi (IAM, VPC & EC2)
- **Bảo mật:** Làm việc với IAM qua dòng lệnh giúp tôi nhanh chóng liệt kê User, Group và Policy. Tôi có thể quản lý thông tin IAM bằng các câu lệnh CLI và hiểu cách sử dụng CLI để kiểm tra quyền truy cập của các thực thể.
- **Mạng:** CLI cho phép xuất cấu trúc mạng dưới dạng JSON. Tôi đã biết kiểm tra thông tin VPC, liệt kê Subnet và Security Group, và quản lý tài nguyên mạng thông qua AWS CLI để hỗ trợ cho việc khắc phục sự cố mạng.
- **Điện toán:** Đây là phần thú vị nhất. Thay vì qua nhiều màn hình cấu hình, tôi đã khởi tạo EC2 Instance bằng AWS CLI chỉ với một dòng lệnh duy nhất chứa các cờ (flags) cần thiết. Sau đó, tôi kiểm tra trạng thái Instance và thực hiện các thao tác quản lý EC2 từ dòng lệnh.

---

### Trải nghiệm Thực hành: Phân tích các Module

**Module 1 & 2 — Nền tảng (Introduction & Installation)**
- Bắt đầu bằng việc đọc tài liệu giới thiệu AWS CLI và tìm hiểu kiến trúc và nguyên lý hoạt động (REST API requests).
- Tiến hành chuẩn bị môi trường thực hành, tải binary và cài đặt AWS CLI.
- Thiết lập định danh cá nhân bằng cách cấu hình thông tin tài khoản AWS.
- Dùng lệnh để kiểm tra phiên bản và kết nối.

**Module 3 & 4 — Khám phá và Lưu trữ (Check Resource & S3)**
- Gọi API để kiểm tra thông tin tài nguyên AWS.
- Thực hành các lệnh AWS CLI cơ bản và làm quen với cú pháp CLI.
- Với dịch vụ lưu trữ, tôi dùng lệnh `mb` (make bucket) để tạo Bucket.
- Dùng `cp` và `sync` để upload và Download tệp. Cuối cùng, dọn dẹp bằng cách xóa dữ liệu trong Bucket.

**Module 5 & 6 — Dịch vụ tích hợp (SNS & IAM)**
- Khởi tạo hệ thống pub/sub bằng lệnh tạo Topic.
- Liên kết endpoint bằng cách tạo Subscription và gửi thông báo thử nghiệm.
- Trong IAM, tôi dùng lệnh để kiểm tra User, liệt kê Group và Policy, và thực hành các lệnh IAM khác để kiểm toán hệ thống.

**Module 7 & 8 — Hạ tầng tính toán (VPC & EC2)**
- Xuất dữ liệu mạng bằng cách kiểm tra VPC, xem Subnet, và kiểm tra Security Group.
- Cung cấp tài nguyên tính toán bằng lệnh `run-instances` để khởi tạo EC2 Instance.
- Gọi lệnh `describe-instances` để kiểm tra trạng thái Instance và thực hiện quản lý EC2 bằng AWS CLI.

**Module 9 — Kỷ luật dọn dẹp (Cleanup Resources)**
- Truy vấn để kiểm tra toàn bộ tài nguyên đã tạo.
- Dùng các lệnh `terminate`, `delete` để xóa tài nguyên không còn sử dụng.
- Chạy lại các lệnh `describe` để xác nhận hoàn tất Cleanup.

---

### Đánh giá mức độ hoàn thành Tuần 8:

- Hoàn toàn hiểu vai trò của AWS CLI trong việc quản lý dịch vụ AWS.
- Thực thi thành thạo cài đặt và cấu hình AWS CLI.
- Đã thực hành thành công quản lý Amazon S3 bằng CLI.
- Tích hợp và biết sử dụng AWS CLI với Amazon SNS.
- Khai thác dữ liệu để quản lý được IAM và VPC thông qua dòng lệnh.
- Khởi tạo và quản lý EC2 bằng AWS CLI một cách nhanh chóng.
- Nhìn chung, tôi đã nâng cao kỹ năng sử dụng AWS CLI để tự động hóa các thao tác quản trị trên AWS.

---

### Những khó khăn và Rào cản kỹ thuật:

- **Rào cản ngôn ngữ máy:** Ban đầu chưa quen với cú pháp và tham số của AWS CLI, đặc biệt là các tham số truyền vào dưới dạng mảng JSON.
- **Xung đột bộ nhớ:** Hệ sinh thái lệnh rất rộng dẫn đến việc dễ nhầm lẫn giữa các lệnh của từng dịch vụ AWS (ví dụ: `aws s3` vs `aws s3api`).
- **Lỗi phân quyền:** Không thể thực thi lệnh vì một số thao tác yêu cầu cấu hình IAM Permission phù hợp.
- **Sự bất tiện của CLI:** Khác với GUI, việc ghi nhớ tên tài nguyên và ID khi thao tác bằng CLI còn mất thời gian (ví dụ: phải copy/paste VPC ID, Subnet ID).

---

### Hướng khắc phục và Giải pháp:

- **Tạo phản xạ cơ bắp:** Cách duy nhất để giỏi CLI là thực hành thường xuyên các lệnh AWS CLI.
- **Khai thác tài liệu:** Thay vì học thuộc lòng, tôi học cách tham khảo AWS CLI Command Reference khi cần hoặc sử dụng cờ `help`.
- **Bảo mật đi trước:** Luôn kiểm tra IAM Policy trước khi thực hiện các thao tác để đảm bảo Access Key có đủ quyền.
- **Xây dựng thư viện cá nhân:** Chủ động ghi chú các câu lệnh thường dùng để thuận tiện trong quá trình thực hành.

---

### Định hướng mở rộng cho tuần tiếp theo:

Hành trình tự động hóa sẽ bước lên một tầm cao mới. Việc gõ từng lệnh CLI vẫn mang tính chất thủ công (Imperative). Tuần sau, chúng ta sẽ chuyển sang mô hình khai báo (Declarative):
- Chuyển hướng nghiên cứu để tìm hiểu về AWS CloudFormation.
- Áp dụng kỹ năng lập trình để thực hành tạo hạ tầng dưới dạng mã (Infrastructure as Code).
- Thiết kế và triển khai tài nguyên AWS bằng Template (YAML/JSON).
- Tìm hiểu quản lý Stack và cập nhật hạ tầng một cách an toàn và có kiểm soát.
- Cuối cùng, chuẩn bị hình ảnh minh chứng và hoàn thiện báo cáo thực hành tuần tiếp theo.