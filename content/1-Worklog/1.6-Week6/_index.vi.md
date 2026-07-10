---
title: "Worklog Tuần 6"
date: 2026-05-22
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu tuần 6: Định hình tư duy Observability trong vận hành hạ tầng

Trong tuần thứ 6 của chương trình cloud journey 12 tuần này, mục tiêu cốt lõi đã chuyển dịch từ việc triển khai tài nguyên sang việc thiết lập "đôi mắt thần" cho toàn bộ kiến trúc. Là một lập trình viên, việc đưa mã nguồn lên server là chưa đủ; việc duy trì và thấu hiểu trạng thái hệ thống là yếu tố sống còn. Các mục tiêu trọng điểm bao gồm:

- **Khám phá nền tảng giám sát:** Tìm hiểu tổng quan về Amazon CloudWatch và hiểu rõ vai trò của CloudWatch trong việc giám sát tài nguyên và ứng dụng trên AWS.
- **Đo lường hiệu năng cốt lõi:** Thực hành sử dụng CloudWatch Metrics để theo dõi hiệu năng hệ thống, từ đó đánh giá được tình trạng sức khỏe thực tế của các máy chủ và dịch vụ.
- **Làm chủ công cụ phân tích dữ liệu:** Tìm hiểu và ứng dụng linh hoạt các cú pháp nâng cao như Search Expressions, Math Expressions và Dynamic Labels để tinh chỉnh và biến đổi dữ liệu thô thành các chỉ số có ý nghĩa.
- **Khai thác nhật ký hệ thống:** Khám phá chuyên sâu vào CloudWatch Logs và khả năng truy vấn mạnh mẽ của CloudWatch Logs Insights. Bứt phá giới hạn bằng cách tạo Metric Filters từ dữ liệu log, biến những dòng văn bản tĩnh thành các biểu đồ động.
- **Tự động hóa phản ứng sự cố:** Tiến hành cấu hình CloudWatch Alarms để theo dõi và cảnh báo sự cố, giúp đội ngũ vận hành phản ứng theo thời gian thực (real-time) trước khi ứng dụng sập hoàn toàn.
- **Trực quan hóa và Tối ưu:** Xây dựng CloudWatch Dashboards để trực quan hóa dữ liệu giám sát quy tụ về một màn hình duy nhất. Cuối cùng, thực hiện dọn dẹp tài nguyên sau khi hoàn thành bài thực hành nhằm tối ưu chi phí và nâng cao kỹ năng giám sát và quản lý hệ thống trên AWS.

---

### Lộ trình và các công việc triển khai trong tuần:

| Thứ | Hạng mục công việc chuyên sâu | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 2 | - **Nghiên cứu nền tảng:** Đọc tổng quan workshop Amazon CloudWatch. <br> - Phân tích lý thuyết để tìm hiểu vai trò của CloudWatch trong AWS như một trung tâm dữ liệu tập trung. <br> - Chuẩn bị môi trường thực hành bằng cách khởi tạo các tài nguyên cần thiết. | 08/06/2026 | 08/06/2026 | https://000008.awsstudygroup.com/1-introduction/ |
| 3 | - **Khai thác Metrics:** Bắt đầu tìm hiểu CloudWatch Metrics để thu thập số liệu. <br> - Trực tiếp xem và phân tích Metrics từ các tài nguyên đang chạy. <br> - Thực hành Search Expressions để lọc và tìm kiếm chính xác các chỉ số bị ẩn sâu. | 09/06/2026 | 09/06/2026 | https://000008.awsstudygroup.com/3-cloud-watch-metric/ |
| 4 | - **Biến đổi Dữ liệu:** Thực hành Math Expressions để thực hiện các phép toán (cộng, trừ, tính tỷ lệ) trên nhiều luồng Metrics. <br> - Sử dụng Dynamic Labels để biểu đồ tự động hiển thị tên tài nguyên thay vì các ID khô khan. <br> - Trực quan hóa dữ liệu Metrics để dễ dàng đánh giá xu hướng hiệu năng. | 10/06/2026 | 10/06/2026 | https://000008.awsstudygroup.com/3-cloud-watch-metric/ |
| 5 | - **Quản trị Nhật ký:** Làm việc với CloudWatch Logs để thu thập đầu ra của ứng dụng. <br> - Viết các câu lệnh truy vấn log bằng CloudWatch Logs Insights nhằm tìm kiếm nguyên nhân gốc rễ (root cause). <br> - Thiết lập và tạo Metric Filters từ Logs để đếm số lần xuất hiện của các từ khóa báo lỗi. | 11/06/2026 | 11/06/2026 | https://000008.awsstudygroup.com/4-cloud-watch-logs/ |
| 6 | - **Hệ thống Cảnh báo:** Tạo CloudWatch Alarms dựa trên các ngưỡng sinh tử của hệ thống. <br> - Tích hợp và cấu hình SNS Notifications để đẩy luồng cảnh báo qua email/SMS. <br> - Chủ động kiểm tra hoạt động của Alarms bằng cách giả lập tải trọng cao. | 12/06/2026 | 12/06/2026 | https://000008.awsstudygroup.com/5-cloud-watch-alarm/ |
| 7 | - **Quy tụ Thông tin:** Xây dựng CloudWatch Dashboards chuyên nghiệp. <br> - Tùy chỉnh bằng cách thêm Metrics và Alarms vào Dashboard. <br> - Tạo ra một giao diện duy nhất để theo dõi dữ liệu tập trung. | 13/06/2026 | 13/06/2026 | https://000008.awsstudygroup.com/6-cloud-watch-dashboard/ |
| CN | - **Bảo trì và Đúc kết:** Kiểm tra các tài nguyên đã tạo trong suốt quá trình. <br> - Nghiêm túc thực hiện Cleanup Resources để bảo vệ hóa đơn AWS. <br> - Tổng kết kiến thức đã học trong tuần để chuyển hóa thành kinh nghiệm thực chiến. | 14/06/2026 | 14/06/2026 | https://000008.awsstudygroup.com/7-clean-up/ |

---

### Kết quả đạt được tuần 6: Đúc kết lý thuyết chuyên sâu

#### 1. Kiến trúc hệ sinh thái Amazon CloudWatch
Trải qua quá trình nghiên cứu, tôi hiểu Amazon CloudWatch là dịch vụ giám sát và quan sát hệ thống trên AWS. Nó đóng vai trò như một hệ thần kinh trung ương, liên tục lắng nghe nhịp đập của hạ tầng. Bằng cách biết cách thu thập và phân tích dữ liệu từ Metrics và Logs, người quản trị có thể dự đoán trước các nguy cơ hỏng hóc. Do đó, tôi hoàn toàn hiểu tầm quan trọng của việc giám sát tài nguyên và ứng dụng để đảm bảo tính sẵn sàng cao (High Availability).

#### 2. Phân tích Dữ liệu Đo lường (CloudWatch Metrics)
Metrics là những con số biết nói. Tôi đã biết cách xem và phân tích Metrics như CPU Utilization hay Network In/Out. Tuy nhiên, khi hệ thống phình to, việc tìm kiếm thủ công là bất khả thi. Vì vậy, tôi đã hiểu cách sử dụng Search Expressions để lọc dữ liệu một cách vô cùng hiệu quả. Vượt lên trên dữ liệu thô, tôi có thể sử dụng Math Expressions để tính toán dữ liệu Metrics (ví dụ: tính toán tỷ lệ lỗi bằng công thức `Errors / RequestCount`). Để giao diện thân thiện hơn với con người, tôi áp dụng Dynamic Labels để hiển thị dữ liệu trực quan hơn.

#### 3. Khai thác sức mạnh của CloudWatch Logs
Nhật ký hệ thống chứa mọi sự thật về ứng dụng. Tôi hiểu cách thu thập và lưu trữ Logs vào các Log Groups. Điểm đột phá là khi hệ thống gặp lỗi, thay vì đọc hàng triệu dòng text, tôi biết cách truy vấn Logs bằng CloudWatch Logs Insights thông qua các câu lệnh SQL-like. Một kỹ thuật xuất sắc khác là tạo Metric Filters từ các sự kiện Log, giúp tự động quét các log stream, bắt các từ khóa như "Exception" và chuyển đổi chúng thành một Metric đếm số lượng lỗi theo thời gian thực.

#### 4. Phản ứng tự động với CloudWatch Alarms
Việc ngồi nhìn màn hình cả ngày là không thực tế. Tôi đã thấu hiểu cơ chế hoạt động của CloudWatch Alarms. Hệ thống này hoạt động theo nguyên tắc máy trạng thái (OK, ALARM, INSUFFICIENT_DATA). Bằng cách biết cách thiết lập ngưỡng cảnh báo phù hợp, báo động sẽ được kích hoạt nếu hệ thống vượt ranh giới an toàn. Đi kèm với đó, việc cấu hình SNS để nhận thông báo khi có sự cố là mắt xích cuối cùng, giúp chuyển tiếp tín hiệu cảnh báo đến hòm thư của kỹ sư trực hệ thống.

#### 5. Bảng điều khiển trung tâm (CloudWatch Dashboards)
Để giải quyết vấn đề phân mảnh thông tin, tôi tiến hành tạo Dashboard để theo dõi hệ thống. Bằng cách hiển thị Metrics và Alarms trên cùng một giao diện, người quản trị có được một "single pane of glass" (góc nhìn toàn cảnh duy nhất), hỗ trợ theo dõi hiệu suất hệ thống theo thời gian thực cực kỳ đắc lực.

---

### Trải nghiệm Thực hành: Mô phỏng từng bước triển khai

**Module 1 — Khởi động hệ thống (Introduction)**
- Truy cập Amazon CloudWatch từ bảng điều khiển AWS.
- Dành thời gian tìm hiểu kiến trúc và chức năng chính của CloudWatch qua các sơ đồ luồng dữ liệu.
- Bắt tay chuẩn bị môi trường thực hành, thiết lập một vài phiên bản EC2 làm mục tiêu theo dõi.

**Module 2 — Tinh chỉnh các số liệu đo lường (CloudWatch Metrics)**
- Trực tiếp xem Metrics của tài nguyên AWS để đánh giá mức tiêu thụ CPU.
- Vận dụng cú pháp mã hóa để sử dụng Search Expressions, gọi ra các thông số mạng nội bộ.
- Triển khai thực hành Math Expressions để vẽ biểu đồ so sánh giữa trung bình tải và tải tối đa.
- Cấu hình Dynamic Labels để nhãn biểu đồ tự động phản ánh tên của máy chủ thay vì dải IP.

**Module 3 — Quản trị Log hệ thống (CloudWatch Logs)**
- Tạo và quản lý Log Groups để phân loại log của web server và database riêng biệt.
- Viết query để truy vấn Logs bằng Logs Insights, lọc ra 20 lỗi 404 gần nhất trong vòng 1 giờ qua.
- Thiết lập và tạo Metric Filters để quét từ khóa "Error", biến nó thành chỉ số đếm liên tục trên biểu đồ.

**Module 4 — Xây dựng rào chắn báo động (CloudWatch Alarms)**
- Dựa trên Metric Filter vừa tạo, tôi thao tác tạo Alarm mới.
- Liên kết với dịch vụ gửi tin nhắn bằng cách cấu hình SNS Notification và xác nhận đăng ký email.
- Giả lập lỗi trên server và kiểm tra trạng thái Alarm chuyển sang màu đỏ, đồng thời kiểm tra hộp thư đến.

**Module 5 — Giao diện hóa dữ liệu (CloudWatch Dashboards)**
- Khởi tạo Dashboard mới với giao diện lưới (grid).
- Lần lượt thêm Metrics và Alarms vào Dashboard bằng các widget dạng biểu đồ đường (Line chart) và đồng hồ đo (Gauge).
- Tùy chỉnh Widget hiển thị để làm nổi bật các khu vực rủi ro cao.

**Module 6 — Kỷ luật dọn dẹp hệ thống (Cleanup Resources)**
- Rà soát và kiểm tra tài nguyên đã tạo trong toàn bộ các module.
- Tiến hành xóa tài nguyên không cần thiết (Dashboards, Alarms, Log Groups) để cắt đứt các khoản phí lưu trữ.
- Xác nhận hoàn tất Cleanup với một bảng điều khiển gọn gàng.

---

### Đánh giá mức độ hoàn thành tuần 6:

- Hiểu vai trò của Amazon CloudWatch trong AWS như một xương sống của hệ thống vận hành.
- Biết cách sử dụng Metrics, Logs và Alarms một cách nhuần nhuyễn.
- Đã thực hành thành công Search Expressions và Math Expressions để nâng cao khả năng phân tích biểu đồ.
- Nắm vững chu trình tạo được Metric Filters và CloudWatch Alarms.
- Xây dựng được CloudWatch Dashboard hoàn chỉnh có giá trị ứng dụng cao.
- Qua đó, nâng cao kỹ năng giám sát và xử lý sự cố trên AWS ở cấp độ chuyên nghiệp.

---

### Khó khăn và Rào cản phân tích:

- **Logic liên kết:** Ở giai đoạn đầu, tôi cảm thấy khá khó hiểu mối quan hệ giữa Metrics, Logs và Metric Filters. Quá trình từ log thô trở thành một biểu đồ cảnh báo đòi hỏi sự liền mạch về tư duy.
- **Cú pháp phức tạp:** Việc sử dụng Search Expressions và Math Expressions ban đầu còn phức tạp do cấu trúc ngôn ngữ riêng biệt, rất dễ gõ sai biến số.
- **Truy vấn Logs Insights:** Cần thời gian để làm quen với Logs Insights vì nó sử dụng một cú pháp lai giữa SQL và Regex, đòi hỏi phải thử sai (trial and error) nhiều lần.
- **Rủi ro cấu hình luồng thông báo:** Việc cấu hình SNS Notification cần thực hiện chính xác. Nếu chọn sai Topic hoặc quên xác nhận email Subscriptions, Alarm dù có kích hoạt thì thông báo cũng không bao giờ tới tay người quản trị.

---

### Hướng khắc phục và Giải pháp:

- **Nghiên cứu sâu:** Đọc kỹ tài liệu workshop và tài liệu AWS CloudWatch để hệ thống hóa lại các khái niệm qua sơ đồ.
- **Học qua thực hành:** Biến lý thuyết thành phản xạ bằng cách thực hành nhiều lần với Metrics và Logs trên các môi trường giả lập khác nhau.
- **Thử nghiệm từng phần:** Luôn kiểm tra cấu hình SNS trước khi thử nghiệm Alarms bằng cách gửi các tin nhắn test thủ công qua giao diện SNS.
- **Kế thừa kiến thức:** Tích cực tham khảo ví dụ thực tế từ AWS Documentation để copy các mẫu query Logs Insights hiệu quả, tiết kiệm thời gian gỡ lỗi.

---

### Định hướng mở rộng cho tuần tiếp theo:

Hành trình chinh phục Cloud sẽ chuyển sang một trong những trụ cột quan trọng nhất: Bảo mật (Security).
- Chuyển hướng nghiên cứu để tìm hiểu AWS Identity and Access Management (IAM).
- Trực tiếp thực hành tạo User, Group và Policy dựa trên nguyên tắc đặc quyền tối thiểu (Least Privilege).
- Nâng cấp độ khó bằng cách tìm hiểu cơ chế MFA và bảo mật tài khoản AWS.
- Đi sâu nghiên cứu quản lý quyền truy cập trên môi trường Cloud để đảm bảo kiến trúc mạng bất khả xâm phạm.
- Cuối cùng, tiếp tục chuẩn bị hình ảnh minh chứng và hoàn thiện báo cáo thực hành tuần tiếp theo.