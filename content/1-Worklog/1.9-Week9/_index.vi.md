---
title: "Worklog Tuần 9"
date: 2026-06-11
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### Mục tiêu tuần 9: Nhìn lại kiến trúc qua lăng kính "người dùng dịch vụ" thay vì "người viết code"

Sau nhiều tuần tập trung viết code, sửa lỗi và chạy thử nghiệm cho dự án InboxIQ, tuần 9 là lúc dừng lại để **tổng hợp và tra cứu lại bản chất từng dịch vụ AWS đã thực sự đưa vào sản phẩm**. Mục tiêu không phải học một dịch vụ mới, mà là hiểu sâu hơn *tại sao* mỗi dịch vụ được chọn, nó thay thế cho cách làm thủ công nào, và giới hạn/rủi ro của nó là gì. Đây là bước chuẩn bị quan trọng cho phần bảo vệ báo cáo, vì người chấm chắc chắn sẽ hỏi "tại sao dùng X mà không dùng Y".

- Rà soát toàn bộ 5 layer kiến trúc InboxIQ (User, Backend, Workflow, Storage, Monitoring) và liệt kê chính xác dịch vụ nào đang chạy thật trong tài khoản.
- Tìm hiểu sâu vai trò của Amazon Cognito trong việc xác thực người dùng, so sánh với phương án tự viết hệ thống JWT thủ công.
- Phân tích lý do tách hai Lambda (Producer/Worker) và một Lambda phụ trợ (ws-whoami) thay vì gộp toàn bộ logic vào một hàm duy nhất.
- Hiểu rõ cơ chế Amazon API Gateway ở cả hai chế độ REST và WebSocket, vì đây là dịch vụ hiếm khi được dùng đồng thời cả hai chế độ trong một dự án sinh viên.
- Đào sâu vai trò "tấm đệm" (buffer) của Amazon SQS và Dead-Letter Queue trong việc tách rời tốc độ xử lý của client và của AI.
- Ôn lại thiết kế 6 bảng DynamoDB, đặc biệt là chiến lược dùng TTL để tự động dọn dữ liệu thay vì phải viết cron job xóa thủ công.
- Tìm hiểu vì sao thông tin nhạy cảm (OpenAI key, Gmail OAuth secret) được tách riêng vào Secrets Manager và SSM Parameter Store thay vì để trong biến môi trường Lambda.
- Ôn lại vai trò giám sát của CloudWatch và X-Ray trong việc truy vết một request đi qua nhiều Lambda bất đồng bộ.
- Đối chiếu toàn bộ dịch vụ đã dùng với chi phí Free Tier thực tế, chuẩn bị số liệu cho phần "chi phí ước tính" của báo cáo.

---

### Các công việc cần triển khai trong tuần này:

| Thứ | Hạng mục công việc chuyên sâu | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 2 | - Vẽ lại sơ đồ 5 layer kiến trúc trên giấy, đối chiếu từng ô với tài nguyên thật trong AWS Console. <br> - Tìm hiểu lại tài liệu chính thức về Amazon Cognito User Pool: luồng đăng ký, đăng nhập, cấp JWT. <br> - Đối chiếu với cách `AuthService` trong Flutter gọi trực tiếp Cognito. | 22/06/2026 | 22/06/2026 | https://docs.aws.amazon.com/cognito/ |
| 3 | - Nghiên cứu tài liệu AWS Lambda về giới hạn thời gian chạy, cold start và concurrency. <br> - Phân tích lý do tách Producer/Worker: Producer chỉ trả `202 Accepted` nhanh, Worker xử lý nặng (gọi Gmail + OpenAI) chạy nền. <br> - Tìm hiểu vì sao cần thêm Lambda `ws-whoami` riêng cho route WebSocket. | 23/06/2026 | 23/06/2026 | https://docs.aws.amazon.com/lambda/ |
| 4 | - Tìm hiểu tài liệu Amazon API Gateway: sự khác biệt giữa REST API và WebSocket API. <br> - Nghiên cứu vòng đời kết nối WebSocket (`$connect`, `$disconnect`, custom route) và lý do `$connect` không push được message. <br> - Đối chiếu Lambda Authorizer với việc xác thực JWT trên từng request REST. | 24/06/2026 | 24/06/2026 | https://docs.aws.amazon.com/apigateway/ |
| 5 | - Nghiên cứu Amazon SQS: Standard Queue, Visibility Timeout, redrive policy và Dead-Letter Queue. <br> - Tìm hiểu Partial Batch Response của SQS-Lambda trigger, vì sao nó tránh được việc xử lý lại toàn bộ batch khi chỉ 1 message lỗi. <br> - Tìm hiểu Amazon EventBridge Scheduler và mô hình cron-based invoke. | 25/06/2026 | 25/06/2026 | https://docs.aws.amazon.com/sqs/ <br> https://docs.aws.amazon.com/eventbridge/ |
| 6 | - Ôn lại thiết kế bảng DynamoDB: Partition Key, Sort Key, Global Secondary Index (nếu có) và cơ chế TTL tự xóa dữ liệu. <br> - Đối chiếu 6 bảng thực tế (`users`, `user-settings`, `gmail-connections`, `email-summaries`, `processing-jobs`, `ws-connections`) với mục đích sử dụng của từng bảng. <br> - Xác nhận bảng nào đang thực sự được ghi/đọc trong code, bảng nào mới chỉ khai báo trong SAM template. | 26/06/2026 | 26/06/2026 | https://docs.aws.amazon.com/dynamodb/ |
| 7 | - Tìm hiểu AWS Secrets Manager và Systems Manager Parameter Store: khi nào dùng cái nào, chi phí khác nhau ra sao. <br> - Nghiên cứu cơ chế cache secret ở global scope trong Lambda để tránh gọi Secrets Manager mỗi lần invoke (giảm chi phí + độ trễ). <br> - Ôn lại CloudWatch Logs/Metrics và AWS X-Ray tracing giữa các Lambda bất đồng bộ. | 27/06/2026 | 27/06/2026 | https://docs.aws.amazon.com/secretsmanager/ <br> https://docs.aws.amazon.com/xray/ |
| CN | - Tổng hợp toàn bộ dịch vụ đã dùng thành một bảng tra cứu nhanh (dịch vụ – vai trò – thay thế cho gì – rủi ro). <br> - Đối chiếu với Cost Explorer/Billing Dashboard để xác nhận số liệu chi phí thực tế trong Free Tier. <br> - Viết báo cáo tổng kết tuần: kết quả, khó khăn, hướng khắc phục và bài học rút ra. | 28/06/2026 | 28/06/2026 | Nội bộ dự án InboxIQ |

---

### Kết quả đạt được tuần 9: Bản đồ tra cứu dịch vụ đã áp dụng vào InboxIQ

#### 1. Lớp xác thực — Amazon Cognito

Việc lùi lại tìm hiểu Cognito sau khi đã tích hợp xong giúp tôi hiểu rõ hơn *tại sao* nó đáng dùng hơn tự viết hệ thống JWT. Cognito User Pool đảm nhiệm toàn bộ vòng đời: đăng ký, xác thực email, đăng nhập, cấp/làm mới JWT, mà không cần tôi tự lưu trữ mật khẩu hay xử lý hashing. Trong `AuthService` của app Flutter, việc gọi thẳng Cognito (không qua API Gateway) là lựa chọn hợp lý vì Cognito đã tự expose endpoint xác thực an toàn — API Gateway chỉ cần xác thực JWT ở các API nghiệp vụ phía sau (Producer). Đây là điểm tôi từng ghi nhầm trong tài liệu kiến trúc ở tuần trước và đã điều chỉnh lại cho khớp với code thật.

#### 2. Lớp tính toán — AWS Lambda (Producer / Worker / ws-whoami)

Đọc lại tài liệu Lambda giúp tôi diễn giải rõ ràng hơn quyết định tách 3 hàm thay vì 1:

- **Lambda Producer**: chỉ làm một việc — nhận request, đóng gói message kèm `connectionId`, đẩy vào SQS và trả `202 Accepted` ngay. Việc này giữ thời gian phản hồi API cực ngắn, tránh timeout phía client.
- **Lambda Worker**: xử lý nặng (gọi Gmail API, gọi OpenAI, ghi DynamoDB, push WebSocket), được trigger bất đồng bộ từ SQS nên có thể chạy lâu hơn giới hạn timeout của một API Gateway request thông thường mà không ảnh hưởng trải nghiệm người dùng.
- **Lambda ws-whoami**: ra đời từ một hạn chế thực tế của API Gateway WebSocket — route `$connect` không đảm bảo push được message về client ngay sau khi kết nối. Tách một route riêng để app chủ động hỏi lại `connectionId` là cách giải quyết đúng bản chất kiến trúc, không phải một bản vá tạm thời.

Việc tách 3 Lambda cũng phù hợp với nguyên tắc IAM Least Privilege: mỗi hàm chỉ được cấp đúng quyền cần thiết (Producer không cần quyền gọi Gmail/OpenAI, Worker không cần quyền ghi vào SQS Main ngoài việc nhận trigger).

#### 3. Lớp cổng vào — Amazon API Gateway (REST + WebSocket)

Đây là dịch vụ khiến tôi bất ngờ nhất khi đọc lại tài liệu, vì phần lớn dự án sinh viên chỉ dùng một chế độ REST hoặc WebSocket, còn InboxIQ dùng cả hai cho hai mục đích khác nhau:

- **REST API**: nhận yêu cầu "Check Gmail" — mô hình request/response cổ điển, phù hợp vì client chủ động khởi tạo hành động.
- **WebSocket API**: dùng để đẩy kết quả AI về app theo thời gian thực, vì kết quả xử lý AI mất vài giây đến vài chục giây — nếu dùng polling REST liên tục sẽ tốn tài nguyên và trải nghiệm giật cục hơn nhiều.

Lambda Authorizer xác thực JWT ở tầng REST giúp tách hoàn toàn logic xác thực khỏi logic nghiệp vụ trong Producer.

#### 4. Lớp workflow bất đồng bộ — Amazon SQS và EventBridge

Đọc lại tài liệu SQS giúp tôi gọi tên chính xác lý do hệ thống ổn định hơn khi có hàng đợi ở giữa: SQS đóng vai trò "tấm đệm" tách rời tốc độ request đến (có thể dồn dập) khỏi tốc độ Worker có thể xử lý (giới hạn bởi rate limit của OpenAI/Gmail). Cơ chế **Partial Batch Response** đặc biệt quan trọng — khi Worker xử lý một batch nhiều message, nếu chỉ một message lỗi, SQS chỉ đẩy lại đúng message đó thay vì toàn bộ batch, tránh xử lý trùng lặp không cần thiết. Sau 3 lần retry thất bại, message tự động chuyển sang Dead-Letter Queue để không kẹt hàng đợi chính mãi mãi.

EventBridge Scheduler đóng vai trò tùy chọn — bắn message định kỳ (30 phút) vào SQS Main giống hệt một request thật từ người dùng, thay vì trigger thẳng vào Worker. Thiết kế này giúp cả hai luồng (thủ công và tự động) đi qua đúng một cửa duy nhất, giảm nguy cơ có hai đường logic xử lý khác nhau cho cùng một tác vụ.

#### 5. Lớp lưu trữ — Amazon DynamoDB (6 bảng)

Việc rà soát lại 6 bảng giúp tôi nhận ra rõ ràng chiến lược dùng **TTL (Time To Live)** để tự động dọn dữ liệu là một quyết định tiết kiệm công sức đáng kể — không cần viết Lambda cron để xóa dữ liệu cũ, DynamoDB tự xóa item khi hết hạn:

| Bảng | Vai trò | TTL |
|---|---|---|
| `inboxiq-users` | Thông tin user cơ bản | Không có |
| `inboxiq-user-settings` | Cấu hình cá nhân hoá | Không có |
| `inboxiq-gmail-connections` | Lưu Gmail OAuth token | Không có |
| `inboxiq-email-summaries` | Bản tóm tắt email | 30 ngày |
| `inboxiq-processing-jobs` | Trạng thái xử lý (debug) | 7 ngày |
| `inboxiq-ws-connections` | Mapping connectionId ↔ userId | 2 giờ |

Điểm cần lưu ý và trung thực khi bảo vệ báo cáo: bảng `inboxiq-processing-jobs` hiện mới chỉ được khai báo trong SAM template, chưa có đoạn code nào thực sự ghi dữ liệu vào đó — cần ghi rõ đây là bảng dự phòng cho việc debug ở giai đoạn sau, không phải một tính năng đã hoàn thiện.

#### 6. Lớp bảo mật cấu hình — Secrets Manager và SSM Parameter Store

Đọc lại tài liệu giúp tôi phân biệt rõ khi nào dùng dịch vụ nào: **Secrets Manager** dùng cho dữ liệu thực sự nhạy cảm và cần rotation (OpenAI API key), còn **SSM Parameter Store** phù hợp cho cấu hình ít nhạy cảm hơn hoặc không cần rotation tự động, với chi phí thấp hơn đáng kể. Việc cache secret ở **global scope** của Lambda (bên ngoài handler function) là một chi tiết kỹ thuật quan trọng — giúp secret chỉ được lấy một lần khi container Lambda khởi động (cold start), các lần invoke sau tái sử dụng container sẽ dùng lại giá trị đã cache, vừa giảm độ trễ vừa giảm số lần gọi Secrets Manager (dịch vụ này tính phí theo số lần gọi API).

#### 7. Lớp giám sát — CloudWatch và X-Ray

Vì hệ thống có nhiều Lambda gọi nhau bất đồng bộ qua SQS và WebSocket, việc debug một request cụ thể (ví dụ: vì sao một email không được tóm tắt) không thể chỉ nhìn log của một hàm. CloudWatch Logs lưu log chi tiết từng Lambda, còn X-Ray cho phép nối các đoạn trace lại thành một "hành trình" xuyên suốt Producer → SQS → Worker → DynamoDB/WebSocket, giúp xác định chính xác bước nào bị chậm hoặc lỗi thay vì đoán mò.

---

### Trải nghiệm Thực hành: Đối chiếu tài liệu với hệ thống thật

**Module 1 — Kiểm tra lớp xác thực**
- Mở AWS Console, vào Cognito User Pool đang dùng cho InboxIQ.
- Kiểm tra App Client, xác nhận không bật client secret (bắt buộc với mobile app public client).
- Đối chiếu luồng `InitiateAuth` trong `AuthService` với tài liệu chính thức của Cognito.

**Module 2 — Kiểm tra lớp tính toán**
- Vào Lambda Console, mở lần lượt Producer, Worker, ws-whoami.
- Kiểm tra IAM Role gắn với từng hàm, xác nhận đúng nguyên tắc Least Privilege (mỗi hàm chỉ có quyền tương ứng vai trò).
- Xem lại cấu hình timeout và memory của từng hàm, đối chiếu với đặc thù công việc (Producer timeout ngắn, Worker timeout dài hơn).

**Module 3 — Kiểm tra lớp cổng vào**
- Vào API Gateway Console, kiểm tra route REST (`/check-gmail`) và route WebSocket (`$connect`, `$disconnect`, `whoami`).
- Kiểm tra Lambda Authorizer gắn đúng vào route REST cần xác thực.

**Module 4 — Kiểm tra lớp workflow**
- Vào SQS Console, kiểm tra Main Queue và Dead-Letter Queue, xem redrive policy (maxReceiveCount = 3).
- Vào EventBridge Console, kiểm tra rule Scheduler đang trỏ đúng vào SQS Main Queue.

**Module 5 — Kiểm tra lớp lưu trữ**
- Vào DynamoDB Console, mở từng bảng trong 6 bảng, kiểm tra cấu hình TTL đã bật đúng field chưa.
- Query thử bảng `inboxiq-email-summaries` để xác nhận dữ liệu thật đang được ghi đúng cấu trúc.

**Module 6 — Kiểm tra lớp bảo mật cấu hình và giám sát**
- Vào Secrets Manager, xác nhận OpenAI key được lưu đúng chỗ, không nằm trong biến môi trường Lambda dưới dạng plaintext.
- Vào CloudWatch Logs Insights, chạy thử query lọc log theo `connectionId` để xác nhận có thể truy vết một request cụ thể.
- Mở X-Ray Service Map, xác nhận nhìn thấy đường đi giữa Producer, SQS và Worker.

---

### Đánh giá kết quả tuần 9:

- Xây dựng được một "bản đồ tra cứu" đầy đủ: dịch vụ – vai trò – lý do chọn – rủi ro, cho toàn bộ 5 layer kiến trúc InboxIQ.
- Củng cố vững chắc lý do kỹ thuật đằng sau từng quyết định thiết kế, sẵn sàng trả lời câu hỏi "tại sao dùng X" khi bảo vệ báo cáo.
- Phát hiện và ghi nhận trung thực một điểm chưa hoàn thiện: bảng `inboxiq-processing-jobs` mới chỉ tồn tại ở tầng hạ tầng, chưa có logic ghi dữ liệu.
- Làm rõ hơn sự khác biệt giữa Secrets Manager và SSM Parameter Store, áp dụng đúng dịch vụ cho đúng loại dữ liệu.
- Xác nhận lại chi phí thực tế vẫn nằm trong Free Tier + chi phí OpenAI API ở mức thấp như ước tính ban đầu.

---

### Khó khăn gặp phải trong quá trình rà soát:

- Một số ghi chú kiến trúc cũ (viết ở tuần trước) không khớp hoàn toàn với code thật — ví dụ mô tả sai luồng App gọi Cognito qua API Gateway, trong khi thực tế App gọi thẳng Cognito.
- Khó phân biệt rạch ròi lúc nào nên dùng Secrets Manager, lúc nào dùng SSM Parameter Store nếu chỉ đọc tài liệu mà không đối chiếu với chi phí thực tế của từng dịch vụ.
- Việc truy vết một request bất đồng bộ qua nhiều Lambda bằng X-Ray đòi hỏi phải hiểu rõ khái niệm trace segment/subsegment, ban đầu khá rối vì quen nhìn log tuyến tính của một hàm đơn.
- Nhận ra một bảng DynamoDB (`inboxiq-processing-jobs`) đã khai báo nhưng chưa dùng, dễ gây hiểu lầm nếu không kiểm tra kỹ trước khi viết vào báo cáo.

---

### Hướng khắc phục và Best Practices đúc kết được:

- Luôn đối chiếu tài liệu kiến trúc với Console/code thật trước khi đưa vào báo cáo chính thức, không tin tưởng hoàn toàn ghi chú cũ.
- Ghi rõ trạng thái thực tế của từng tài nguyên (đã dùng / mới khai báo / dự phòng) thay vì mặc định mọi thứ trong SAM template đều đang hoạt động.
- Khi so sánh hai dịch vụ tương tự (Secrets Manager vs SSM Parameter Store), lập bảng so sánh ngắn gọn theo tiêu chí: chi phí, khả năng rotation, mức độ nhạy cảm phù hợp.
- Tập luyện đọc X-Ray Service Map thường xuyên hơn thay vì chỉ dựa vào CloudWatch Logs, để quen với việc truy vết hệ thống bất đồng bộ.
- Duy trì thói quen kiểm tra Billing Dashboard định kỳ dù hệ thống đang nằm trong Free Tier, để phát hiện sớm nếu có dịch vụ nào phát sinh chi phí ngoài dự kiến.

---

### Định hướng tối ưu cho tuần tiếp theo:

- Bổ sung logic thực sự ghi dữ liệu vào bảng `inboxiq-processing-jobs` hoặc cân nhắc loại bỏ khỏi kiến trúc nếu không cần thiết cho MVP.
- Tìm hiểu thêm về AWS Cost Explorer để phân tích chi tiết chi phí theo từng dịch vụ trong InboxIQ, phục vụ phần "chi phí ước tính" của báo cáo tốt nghiệp.
- Cân nhắc bổ sung `WidgetsBindingObserver` ở phía Flutter để tự động reconnect WebSocket khi app resume, thay vì chỉ reconnect khi người dùng bấm nút.
- Rà soát khả năng nâng cấp Lambda runtime từ Node.js 20.x (đã EOL) lên phiên bản mới hơn trước khi nộp báo cáo cuối kỳ.
- Chuẩn bị slide và số liệu so sánh chi phí "tự triển khai" so với "dùng dịch vụ AWS managed" cho từng layer, phục vụ phần thuyết trình bảo vệ đồ án.
