---
title: "Worklog Tuần 10"
date: 2026-06-16
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### Mục tiêu tuần 10: Đặt nền móng kiến trúc serverless cho InboxIQ

Tuần này là tuần khởi động phần backend của dự án nhóm InboxIQ — hệ thống phân loại email bằng AI trên kiến trúc serverless. Với vai trò phụ trách backend và kiến trúc tổng thể, mục tiêu của tôi là dựng được "bộ khung xương sống" của hệ thống: từ sơ đồ kiến trúc trên giấy thành những tài nguyên thật đang chạy trong tài khoản AWS, sẵn sàng cho các thành viên khác cắm phần việc của họ vào (Flutter app, OAuth Gmail) ở các tuần sau.

- Chốt sơ đồ kiến trúc 5 layer (User, Backend, Async Workflow, Storage, Monitoring) cùng cả nhóm, xác định ranh giới công việc từng người.
- Dựng hạ tầng lưu trữ: thiết kế và tạo các bảng DynamoDB với chiến lược TTL tự dọn dữ liệu.
- Dựng hàng đợi SQS Main kèm Dead-Letter Queue với redrive policy, làm "tấm đệm" giữa request người dùng và phần xử lý AI.
- Viết hai Lambda cốt lõi theo mô hình Producer/Worker: Producer nhận request trả về nhanh, Worker xử lý nặng chạy nền qua SQS trigger.
- Đưa toàn bộ hạ tầng vào quản lý bằng AWS SAM (Infrastructure as Code), thay vì tạo tay từng resource trên Console.
- Tích hợp lời gọi OpenAI API (GPT-4o-mini) trong Worker để tóm tắt và phân loại email, lưu key trong Secrets Manager kèm cơ chế cache ở global scope.

---

### Các công việc cần triển khai trong tuần này:

| Thứ | Hạng mục công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 2 | - Họp nhóm chốt kiến trúc 5 layer và phân công: tôi nhận backend + kiến trúc, bạn A nhận Flutter, bạn B nhận OAuth/bảo mật, bạn C nhận tài liệu/kiểm thử. <br> - Vẽ sơ đồ kiến trúc chi tiết trên draw.io, đánh số từng luồng xử lý. | 08/06/2026 | 08/06/2026 | Nội bộ nhóm |
| 3 | - Thiết kế schema các bảng DynamoDB: partition key, sort key, và field TTL cho từng bảng. <br> - Tạo bảng `inboxiq-email-summaries` (TTL 30 ngày), `inboxiq-gmail-connections`, `inboxiq-ws-connections` (TTL 2 giờ), `inboxiq-processing-jobs` (TTL 7 ngày). | 09/06/2026 | 09/06/2026 | https://docs.aws.amazon.com/dynamodb/ |
| 4 | - Tạo SQS Main Queue và Dead-Letter Queue, cấu hình redrive policy maxReceiveCount = 3. <br> - Tìm hiểu Visibility Timeout và mối quan hệ với timeout của Lambda Worker để tránh xử lý trùng message. | 10/06/2026 | 10/06/2026 | https://docs.aws.amazon.com/sqs/ |
| 5 | - Khởi tạo project SAM, viết `template.yaml` phiên bản đầu: khai báo Producer, Worker, SQS trigger với Partial Batch Response. <br> - Viết Lambda Producer: nhận request kèm `connectionId`, đóng gói message đẩy vào SQS, trả `202 Accepted` ngay. | 11/06/2026 | 11/06/2026 | https://docs.aws.amazon.com/serverless-application-model/ |
| 6 | - Viết Lambda Worker phần khung: nhận batch từ SQS, parse message, xử lý lỗi theo mô hình `batchItemFailures`. <br> - Tạo secret `inboxiq/openai-api-key` trong Secrets Manager, viết hàm lấy key có cache ở global scope của Lambda. | 12/06/2026 | 12/06/2026 | https://docs.aws.amazon.com/secretsmanager/ |
| 7 | - Tích hợp lời gọi OpenAI API (GPT-4o-mini) trong Worker: prompt tóm tắt email tiếng Việt, trả JSON gồm summary/priority/category/action. <br> - Viết hàm ghi kết quả vào DynamoDB kèm field TTL `expireAt`. | 13/06/2026 | 13/06/2026 | https://platform.openai.com/docs/ |
| CN | - `sam build && sam deploy` lần đầu, kiểm tra changeset và xác nhận toàn bộ stack `inboxiq-backend` tạo thành công. <br> - Test luồng Producer → SQS → Worker → DynamoDB bằng message giả (chưa có Gmail thật). <br> - Viết báo cáo tổng kết tuần, bàn giao endpoint và cấu trúc message cho bạn A (Flutter) và bạn B (OAuth). | 14/06/2026 | 14/06/2026 | Nội bộ dự án InboxIQ |

---

### Kết quả đạt được tuần 10:

#### 1. Kiến trúc tổng thể được chốt và trở thành "hợp đồng" chung của nhóm

Sơ đồ 5 layer không chỉ là hình vẽ cho báo cáo — nó trở thành tài liệu phân công thực tế: mỗi thành viên nhìn vào biết chính xác ranh giới phần việc của mình và điểm giao tiếp với phần của người khác (ví dụ: bạn A chỉ cần biết Producer nhận body JSON gồm `connectionId` và trả `202`, không cần quan tâm Worker xử lý thế nào). Việc chốt "hợp đồng giao tiếp" sớm giúp cả nhóm làm song song mà không giẫm chân nhau.

#### 2. Mô hình Producer/Worker — quyết định kiến trúc quan trọng nhất tuần

Ban đầu tôi định viết một Lambda duy nhất xử lý tất cả, nhưng khi tính toán thời gian: gọi Gmail API (vài giây) + gọi OpenAI cho nhiều email (có thể vài chục giây) sẽ vượt xa mức timeout hợp lý của một request API Gateway, và người dùng phải nhìn màn hình đứng yên rất lâu. Tách thành Producer (phản hồi tức thì) và Worker (xử lý nền qua SQS) giải quyết triệt để vấn đề này. SQS ở giữa còn đóng vai trò "tấm đệm": nếu nhiều người dùng bấm cùng lúc, request xếp hàng chờ Worker xử lý dần thay vì làm hệ thống quá tải.

#### 3. Partial Batch Response — chi tiết nhỏ nhưng cứu cả batch

Khi Worker nhận một batch nhiều message từ SQS, nếu chỉ một message lỗi mà trả lỗi cho cả batch, SQS sẽ đẩy lại toàn bộ — kể cả những message đã xử lý thành công, gây tóm tắt trùng lặp và tốn phí OpenAI vô ích. Cấu hình `FunctionResponseTypes: ReportBatchItemFailures` kèm việc trả về `batchItemFailures` chỉ chứa message lỗi giúp SQS chỉ retry đúng phần hỏng. Sau 3 lần thất bại, message rơi vào Dead-Letter Queue để không kẹt hàng đợi chính.

#### 4. TTL của DynamoDB — thay thế cả một cron job

Thiết kế field `expireAt` (Unix timestamp) cho từng bảng giúp DynamoDB tự xoá dữ liệu hết hạn: bản tóm tắt email tự biến mất sau 30 ngày, mapping WebSocket connection tự dọn sau 2 giờ. Không cần viết thêm Lambda định kỳ nào để dọn rác — một ví dụ điển hình của việc "để managed service làm việc của nó".

#### 5. Cache secret ở global scope — tiết kiệm cả độ trễ lẫn chi phí

Secrets Manager tính phí theo lượt gọi API. Đặt biến cache bên ngoài handler function giúp key chỉ được lấy một lần khi container Lambda khởi động (cold start); các lần invoke sau trên cùng container dùng lại giá trị đã cache. Chi tiết nhỏ nhưng đúng chuẩn best practice cho mọi Lambda cần secret.

---

### Đánh giá kết quả tuần 10:

- Toàn bộ tầng hạ tầng backend (DynamoDB, SQS, Lambda Producer/Worker, Secrets Manager) đã chạy thật trong tài khoản, quản lý hoàn toàn bằng SAM.
- Luồng bất đồng bộ Producer → SQS → Worker → DynamoDB đã được kiểm chứng với message giả, sẵn sàng ghép với Gmail thật khi bạn B hoàn thành OAuth.
- Bàn giao "hợp đồng giao tiếp" (format message, endpoint) rõ ràng cho hai thành viên phụ trách Flutter và OAuth, mở đường cho làm việc song song từ tuần 8.

---

### Khó khăn gặp phải:

- Lần đầu viết `template.yaml`, dễ nhầm giữa các thuộc tính của `AWS::Serverless::Function` (SAM) và `AWS::Lambda::Function` (CloudFormation thuần) — cú pháp gần giống nhưng không thay thế được cho nhau.
- Xác định Visibility Timeout của SQS phù hợp với timeout của Worker không đơn giản: đặt quá ngắn thì message bị xử lý trùng khi Worker còn đang chạy, đặt quá dài thì message lỗi phải chờ lâu mới được retry.
- Prompt cho GPT-4o-mini phải chỉnh nhiều lần mới trả về JSON ổn định — ban đầu model thỉnh thoảng trả thêm lời dẫn ngoài JSON làm parse lỗi.

---

### Hướng khắc phục và Best Practices đúc kết được:

- Đọc kỹ tài liệu SAM về phần "resource type" trước khi viết template, đối chiếu từng thuộc tính với tài liệu thay vì đoán theo cảm giác.
- Đặt Visibility Timeout của SQS lớn hơn timeout của Lambda Worker (theo khuyến nghị chính thức là gấp ~6 lần) để chắc chắn Worker xử lý xong trước khi message có thể xuất hiện lại.
- Dùng tham số `response_format: json_object` của OpenAI API để ép model chỉ trả JSON, kết hợp ghi rõ schema mong muốn ngay trong system prompt.

---

### Định hướng cho tuần tiếp theo:

- Phối hợp với bạn B tích hợp Gmail OAuth token vào Worker: đọc token từ DynamoDB, xử lý refresh token khi hết hạn.
- Dựng API Gateway WebSocket cho luồng push kết quả real-time về app — phần kiến trúc thử thách nhất còn lại.
- Hỗ trợ bạn A định nghĩa chính xác format message WebSocket mà Flutter cần lắng nghe.
