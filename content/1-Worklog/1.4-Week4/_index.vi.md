---
title: "Worklog Tuần 4"
date: 2026-05-08
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Mục tiêu tuần 4: Xây dựng Kiến trúc Dữ liệu và Tách biệt tầng Ứng dụng

Sau khi làm chủ năng lực tính toán điện toán (EC2), tuần thứ 4 đánh dấu bước ngoặt quan trọng trong việc thiết kế kiến trúc hệ thống phân lớp (Tiered Architecture). Trọng tâm của tuần này là tách biệt tầng dữ liệu (Data Tier) khỏi tầng ứng dụng (Application Tier) bằng cách sử dụng dịch vụ cơ sở dữ liệu được quản lý hoàn toàn. Các mục tiêu chuyên sâu bao gồm:

* **Khám phá Dịch vụ Cơ sở dữ liệu (DBaaS):** Khám phá bức tranh toàn cảnh về Amazon RDS cũng như tầm quan trọng của dịch vụ này trong kiến trúc cơ sở dữ liệu đám mây so với việc tự quản trị (Self-hosted).
* **Nắm bắt Cơ chế Quản trị Tự động:** Hiểu rõ các tính năng cốt lõi của RDS bao gồm: dịch vụ được quản lý (managed service), tự động sao lưu, khả năng mở rộng, kiến trúc Multi-AZ và Read Replica.
* **Quy hoạch Mạng lõi cho Dữ liệu:** Tiến hành thiết lập mạng VPC, Subnet và cấu hình Security Group phục vụ cho cả EC2 và RDS, đảm bảo cơ sở dữ liệu hoàn toàn vô hình trước Internet.
* **Phân vùng Dữ liệu An toàn:** Xây dựng DB Subnet Group nhằm tạo lập không gian mạng chuẩn cho việc triển khai cơ sở dữ liệu có tính sẵn sàng cao (High Availability).
* **Kiến tạo Môi trường Ứng dụng:** Cài đặt và khởi chạy máy ảo EC2 đóng vai trò là server ứng dụng (App Server) kết nối trực tiếp với RDS.
* **Triển khai Dữ liệu Thực chiến:** Thiết lập RDS Database Instance, đồng thời thu thập các thông tin quan trọng như Endpoint, Port và Username để tích hợp hệ thống.
* **Tích hợp Liên hoàn (Integration):** Đưa ứng dụng AWS FCJ Management lên môi trường và cấu hình các biến môi trường để giao tiếp thành công với database RDS.
* **Đảm bảo Tính liên tục (Business Continuity):** Làm quen với các thao tác sao lưu (backup), chụp bản ghi (snapshot) và phục hồi (restore) cơ sở dữ liệu.
* **Kỷ luật Tài chính:** Thực hiện xóa bỏ triệt để các tài nguyên đã khởi tạo sau khi kết thúc bài thực hành nhằm tối ưu chi phí (FinOps).

---

### Các công việc cần triển khai trong tuần này:

| Thứ | Hạng mục công việc chuyên sâu | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - **Nghiên cứu nền tảng:** Đọc tài liệu giới thiệu Amazon RDS. <br> - Làm rõ bản chất hệ thống OLTP, DB Instance, Endpoint. <br> - Phân loại các Database Engine (MySQL, PostgreSQL, Aurora, v.v.). | 11/05/2026 | 11/05/2026 | [https://000005.awsstudygroup.com/](https://000005.awsstudygroup.com/) |
| 3 | - **Thiết kế Mạng phân lớp:** Module 2.1: Create a VPC. <br> - Thiết lập mạng VPC bao gồm cả Public (cho App) và Private Subnet (cho DB). <br> - Trải dài kiến trúc trên nhiều Availability Zone để dự phòng. | 12/05/2026 | 12/05/2026 | [https://000005.awsstudygroup.com/](https://000005.awsstudygroup.com/) |
| 4 | - **Thiết lập Tường lửa:** Module 2.2: Create EC2 Security Group & Module 2.3: Create RDS Security Group. <br> - Định tuyến Security Group chaining: RDS chỉ nhận traffic từ EC2. | 13/05/2026 | 13/05/2026 | [https://000005.awsstudygroup.com/](https://000005.awsstudygroup.com/) |
| 5 | - **Chuẩn bị Hạ tầng:** Module 2.4: Create DB Subnet Group. <br> - Module 3: Create EC2 Instance (App Server). <br> - Kết nối SSH vào máy chủ thông qua MobaXterm. | 14/05/2026 | 14/05/2026 | [https://000005.awsstudygroup.com/](https://000005.awsstudygroup.com/) |
| 6 | - **Khởi tạo Database:** Module 4: Create RDS Database Instance. <br> - Lựa chọn engine, định danh, phân bổ tài nguyên và gắn VPC/Security Group. <br> - Trích xuất Endpoint và Port khi trạng thái Available. | 15/05/2026 | 15/05/2026 | [https://000005.awsstudygroup.com/](https://000005.awsstudygroup.com/) |
| 7 | - **Triển khai Ứng dụng:** Module 5: Application Deployment. <br> - Clone source code, cài Node.js, cấu hình biến môi trường `.env`. <br> - Khởi tạo bảng dữ liệu và chạy ứng dụng web trên cổng 5000. | 16/05/2026 | 16/05/2026 | [https://000005.awsstudygroup.com/](https://000005.awsstudygroup.com/) |
| CN | - **Vận hành & Dọn dẹp:** Module 6: Backup and Restore. <br> - Module 7: Clean up resources (EC2, RDS, Snapshot, SG, VPC) triệt để. | 17/05/2026 | 17/05/2026 | [https://000005.awsstudygroup.com/](https://000005.awsstudygroup.com/) |

---

### Kết quả đạt được Tuần 4: Đúc kết kiến thức chuyên sâu

#### 1. Triết lý Dịch vụ được quản lý (Managed Services)
Thay vì tự cài đặt MySQL trên một máy ảo EC2 (tự quản - Self-managed), tôi đã thấu hiểu sức mạnh của Amazon RDS. Đây là một dịch vụ cơ sở dữ liệu quan hệ được quản lý hoàn toàn (Managed Service). RDS giải phóng kỹ sư khỏi "những công việc nặng nhọc không tạo ra giá trị khác biệt" (undifferentiated heavy lifting) như cài đặt OS, vá lỗi bảo mật (patching), hay thiết lập sao lưu. Nhờ đó, đội ngũ kỹ thuật có thể tập trung hoàn toàn vào việc thiết kế schema và tối ưu hóa truy vấn.

#### 2. Kiến trúc Mạng cho Cơ sở dữ liệu (Database Networking)
Một hệ thống an toàn là hệ thống không phơi mình ra Internet. Tôi nắm vững khái niệm tách biệt tầng ứng dụng (Public Subnet - chứa EC2) và tầng dữ liệu (Private Subnet - chứa RDS). 
Đặc biệt, khái niệm **DB Subnet Group** vô cùng quan trọng: nó là một tập hợp các subnet trải dài trên ít nhất 2 Availability Zones. Điều này bắt buộc AWS phải có không gian để cấp phát tài nguyên dự phòng (Standby Replica) trong kiến trúc Multi-AZ, đảm bảo tính sẵn sàng cao ngay cả khi một trung tâm dữ liệu gặp sự cố vật lý.

#### 3. Chaining Security Group (Bảo mật liên kết)
Đây là kiến thức bảo mật mạng (NetSec) giá trị nhất trong tuần. Thay vì mở port `3306` của RDS cho một dải IP cụ thể, tôi sử dụng cơ chế **Security Group Chaining**. Tôi cấu hình RDS Security Group sao cho Source (Nguồn) chính là ID của EC2 Security Group. Nguyên tắc này tạo ra một vòng tròn tin tưởng: Cơ sở dữ liệu từ chối mọi kết nối ngoại trừ những kết nối phát sinh từ chính các máy chủ ứng dụng của tôi, thiết lập kiến trúc Zero Trust vững chắc.

#### 4. Tích hợp Ứng dụng và Quản lý Cấu hình
Tôi hiểu rằng ứng dụng không bao giờ được hardcode (gắn cứng) thông tin kết nối database vào mã nguồn. Việc sử dụng tệp `.env` để nạp các biến môi trường (DB_HOST, DB_USER, DB_PASS) lúc runtime (thời điểm chạy) giúp ứng dụng linh hoạt. Khi Endpoint của RDS thay đổi (ví dụ sau khi restore snapshot), tôi chỉ cần sửa file `.env` mà không phải biên dịch lại mã nguồn.

#### 5. Phục hồi sau thảm họa (Disaster Recovery)
Tôi nhận thức rõ sự khác biệt giữa Automated Backup (sao lưu tự động theo chu kỳ, hỗ trợ Point-in-time recovery) và Manual Snapshot (bản sao lưu thủ công vĩnh viễn do người dùng tạo). Một bài học vận hành quan trọng: khi phục hồi (Restore) từ Snapshot, AWS không ghi đè lên database cũ mà sẽ tạo ra một DB Instance hoàn toàn mới với một Endpoint mới.

---

### Trải nghiệm Thực hành: Phân tích các Module

**Module 1 & 2 — Khởi tạo Nền tảng Mạng và Tường lửa**
- Bắt đầu với việc thiết lập không gian mạng ảo (VPC), khai báo dải mạng IPv4 CIDR, tạo Public Subnet cho EC2 và Private Subnet cho RDS trên 2 Availability Zones khác biệt.
- Xây dựng Security Group cho EC2 (App Tier) cho phép Inbound cổng `22`, `80`, `443`, và `5000`. Siết chặt bảo mật bằng cách chỉ cho phép SSH từ IP cá nhân.
- Tạo Security Group cho RDS (Data Tier) mở cổng `3306`, chỉ định Source là ID của EC2 Security Group.
- Tạo DB Subnet Group, gom các Private Subnet lại để làm bệ phóng khởi tạo database an toàn.

**Module 3 & 4 — Khởi chạy Application Server và Database**
- **App Server:** Khởi chạy máy ảo Amazon Linux 2023 (`t2.micro` hoặc `t3.micro`), gắn EC2 Security Group, dùng Key Pair để SSH qua MobaXterm.
- **Database:** Khởi chạy RDS Database Instance bằng tùy chọn Standard Create. Định danh DB, khai báo Master user/password, và gắn nó vào VPC, DB Subnet Group, RDS Security Group vừa tạo. Theo dõi trạng thái chuyển từ `Creating` sang `Available` và trích xuất chuỗi kết nối Endpoint.

**Module 5 — Triển khai Ứng dụng Thực chiến (Deployment)**
- SSH vào EC2, cài đặt Git, Clone dự án AWS FCJ Management.
- Thiết lập môi trường thực thi Node.js, cài đặt npm dependencies và MySQL client.
- Tạo tệp `.env` để khai báo `DB_HOST` (là Endpoint của RDS), `DB_NAME`, `DB_USER`, `DB_PASS`.
- Dùng MySQL client test kết nối trực tiếp vào RDS, tạo database `first_cloud_users` và bảng `user`, chèn dữ liệu mẫu.
- Chạy lệnh `npm start` và kiểm thử thành công truy cập ứng dụng web trên trình duyệt qua port `5000`.

**Module 6 & 7 — Sao lưu và Kỷ luật Dọn dẹp (FinOps)**
- Thử nghiệm tính năng tạo Manual Snapshot và khảo sát tiến trình Restore thành một cụm database mới.
- Chấm dứt hoạt động (Terminate) máy ảo EC2.
- Xóa bỏ RDS Database Instance (chú ý bỏ chọn tạo snapshot cuối cùng để tránh phí lưu trữ ngầm).
- Gỡ bỏ lần lượt DB Subnet Group, Security Group, Route Table, IGW và cuối cùng là VPC để trả lại môi trường sạch sẽ.

---

### Những khó khăn và Rào cản kỹ thuật:

- **Lỗi kết nối cơ sở dữ liệu (Connection Timeout):** Ở những lần đầu, ứng dụng không thể kết nối tới RDS. Nguyên nhân phổ biến nhất là quên cấu hình đúng Source trong RDS Security Group (chọn nhầm IP thay vì chọn Security Group của EC2) hoặc đặt nhầm RDS vào Public Subnet.
- **Quản lý biến môi trường:** Đôi khi gõ sai Endpoint hoặc thiếu port trong file `.env`, dẫn đến ứng dụng Node.js văng lỗi "Access Denied" hoặc "Host not found".
- **Độ trễ khởi tạo:** Quá trình tạo RDS mất khá nhiều thời gian (từ 5-10 phút). Điều này dễ gây tâm lý nôn nóng, dẫn đến việc vội vàng thao tác khi database chưa thực sự ở trạng thái `Available`.
- **Rủi ro quên xóa tài nguyên:** RDS là dịch vụ có chi phí khá cao nếu để chạy ngầm. Ngoài việc xóa Instance, những bản Automated Snapshots giữ lại sau khi xóa database cũng sẽ gây phát sinh chi phí lưu trữ EBS.

---

### Hướng khắc phục và Giải pháp (Best Practices):

- **Áp dụng nguyên tắc "Security Group Chaining":** Luôn kiểm tra chéo (Double-check) luật Inbound của RDS. Đảm bảo tuyệt đối không có rule nào chứa `0.0.0.0/0` ở cổng 3306.
- **Log Debugging:** Khi ứng dụng Node.js lỗi, tập thói quen đọc log trên terminal (stdout/stderr) hoặc dùng lệnh `mysql -h <endpoint> -u admin -p` từ EC2 để ping kiểm tra kết nối mạng trước khi đi tìm lỗi trong code.
- **Kỷ luật chờ đợi trạng thái:** Chỉ thực hiện thao tác lấy Endpoint và kết nối khi trạng thái (Status) của RDS chuyển sang màu xanh (`Available`).
- **Checklist Dọn dẹp nghiêm ngặt:** Khi xóa RDS, hệ thống thường hỏi "Create final snapshot?". Đối với môi trường lab, luôn phải bỏ chọn (Uncheck) mục này. Kiểm tra tab "Snapshots" để chắc chắn không còn bản sao lưu nào bị sót lại.

---

### Định hướng mở rộng cho tuần tiếp theo:

Kiến trúc đã hình thành rõ nét. Tuy nhiên, việc vận hành mọi thứ đang phụ thuộc vào việc "click chuột" thủ công và thiếu một cơ chế quản lý chi tiêu tổng thể.
- Bước sang tuần tiếp theo, trọng tâm sẽ dịch chuyển sang **FinOps** với dịch vụ AWS Budgets để học cách thiết lập rào chắn tài chính tự động.
- Tìm hiểu sự khác biệt giữa kiểm soát dòng tiền (Cost) và kiểm soát tài nguyên (Usage).
- Chuẩn bị nền tảng để sau này có thể tự động hóa hạ tầng thay vì tạo thủ công từng Subnet, RDS hay EC2.