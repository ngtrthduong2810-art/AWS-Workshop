---
title: "Worklog Tuần 11"
date: 2026-06-23
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

### Mục tiêu 11: Real-time hoá hệ thống — API Gateway WebSocket và tích hợp Gmail vào Worker

Tuần trước hệ thống mới chạy được với message giả và kết quả nằm im trong DynamoDB. Tuần này có hai mục tiêu lớn: thứ nhất, ghép phần OAuth Gmail (do thành viên phụ trách bảo mật hoàn thành) vào Worker để tóm tắt email thật; thứ hai — và khó hơn nhiều — dựng kênh WebSocket để đẩy kết quả về app theo thời gian thực thay vì bắt app phải liên tục hỏi lại (polling). Đây là tuần tôi phải đọc tài liệu API Gateway nhiều nhất từ đầu dự án, vì WebSocket API có mô hình vận hành khác hẳn REST API quen thuộc.

- Tích hợp Gmail API vào Worker: đọc OAuth token từ DynamoDB, tự động refresh khi token hết hạn (dùng Lambda Layer dùng chung do bạn phụ trách OAuth viết).
- Dựng API Gateway WebSocket với các route `$connect`, `$disconnect` và Lambda Authorizer xác thực JWT qua query string.
- Thiết kế bảng `inboxiq-ws-connections` lưu mapping connectionId ↔ userId để Worker biết push kết quả cho ai.
- Viết logic push kết quả từ Worker về client qua `PostToConnectionCommand`.
- Giải quyết bài toán "client làm sao biết connectionId của chính mình" — dẫn tới quyết định thêm route `whoami` riêng.
- Cập nhật `template.yaml` cho toàn bộ tài nguyên WebSocket, giữ vững nguyên tắc mọi thứ qua Infrastructure as Code.

---

### Các công việc cần triển khai trong tuần này:

| Thứ | Hạng mục công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 2 | - Nhận bàn giao Lambda Layer `gmail-shared` (hàm `refreshAccessToken`) từ bạn phụ trách OAuth. <br> - Tích hợp vào Worker: đọc token từ bảng `inboxiq-gmail-connections`, kiểm tra `expiresAt`, tự refresh khi hết hạn. | 15/06/2026 | 15/06/2026 | Nội bộ nhóm + https://developers.google.com/gmail/api |
| 3 | - Viết hàm `fetchUnreadEmails` trong Worker: gọi Gmail API lấy danh sách email chưa đọc kèm metadata (Subject, From, Date), có AbortController giới hạn thời gian chờ. <br> - Test end-to-end lần đầu với hộp thư Gmail thật: Producer → SQS → Worker → Gmail → OpenAI → DynamoDB. | 16/06/2026 | 16/06/2026 | https://developers.google.com/gmail/api |
| 4 | - Nghiên cứu tài liệu API Gateway WebSocket: mô hình route selection (`$request.body.action`), vòng đời `$connect`/`$disconnect`, và cách backend chủ động push qua Management API. <br> - Tạo WebSocket API `inboxiq-ws` trong `template.yaml`. | 17/06/2026 | 17/06/2026 | https://docs.aws.amazon.com/apigateway/ |
| 5 | - Viết Lambda Authorizer xác thực JWT Cognito truyền qua query string `?token=` lúc `$connect` (WebSocket không gửi được custom header từ trình duyệt/mobile). <br> - Viết Lambda `ws-connect` (lưu connectionId + userId vào bảng, kèm TTL 2 giờ) và `ws-disconnect` (xoá record khi ngắt kết nối). | 18/06/2026 | 18/06/2026 | https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-use-lambda-authorizer.html |
| 6 | - Viết logic push trong Worker: khởi tạo `ApiGatewayManagementApiClient` với endpoint dạng `https://` (không phải `wss://`), gọi `PostToConnectionCommand` gửi payload `{type: "summary-ready", summaries: [...]}`. <br> - Bọc lời gọi push trong try/catch riêng để lỗi push không làm hỏng cả batch xử lý. | 19/06/2026 | 19/06/2026 | https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-how-to-call-websocket-api-connections.html |
| 7 | - Giải bài toán client cần biết connectionId: nghiên cứu và xác nhận `$connect` handler không nên push message ngay (rủi ro GoneException vì connection chưa "sống" tại thời điểm đó). <br> - Thiết kế route `whoami` riêng: client chủ động gửi `{"action": "whoami"}`, Lambda `ws-whoami` trả lại connectionId qua chính connection đó. | 20/06/2026 | 20/06/2026 | https://docs.aws.amazon.com/apigateway/ |
| CN | - Hoàn thiện `template.yaml`: thêm `WsWhoamiFunction`, `WhoamiRoute`, `WhoamiIntegration`, các Lambda Permission tương ứng. <br> - `sam build && sam deploy`, kiểm tra changeset. <br> - Test push WebSocket bằng `wscat` từ máy local, bàn giao format message cho bạn phụ trách Flutter. | 21/06/2026 | 21/06/2026 | Nội bộ dự án InboxIQ |

---

### Kết quả đạt được tuần 11:

#### 1. Worker đã tóm tắt được email thật

Khoảnh khắc đáng nhớ nhất tuần: lần đầu query bảng `inboxiq-email-summaries` và thấy email thật trong hộp thư được GPT-4o-mini phân tích đầy đủ — tóm tắt tiếng Việt, phân loại (work/promo/notification), chấm mức ưu tiên và gợi ý hành động. Chuỗi tích hợp Gmail token (đọc từ DynamoDB, tự refresh khi hết hạn qua Layer dùng chung) hoạt động trơn tru nhờ ranh giới phân công rõ từ tuần trước: bạn phụ trách OAuth lo phần lấy và lưu token, tôi chỉ cần "tiêu thụ" token đúng cách.

#### 2. WebSocket API — mô hình tư duy khác hẳn REST

Điều tôi vỡ ra khi đọc tài liệu: WebSocket API của API Gateway không phải "REST API có kết nối lâu dài" mà là một mô hình hoàn toàn khác. Không có URL path — thay vào đó là **route selection expression** (`$request.body.action`): API Gateway đọc field `action` trong body JSON của message để quyết định route nào xử lý. Backend muốn chủ động gửi message cho client phải đi qua một API quản lý riêng (Management API) với endpoint `https://` kèm connectionId — chứ không phải "trả lời" trực tiếp như response của REST.

Một chi tiết bảo mật đáng ghi nhớ: WebSocket handshake từ mobile/browser không đính kèm custom header được, nên JWT phải truyền qua **query string** và xác thực bằng Lambda Authorizer ở đúng thời điểm `$connect` — một lần duy nhất cho cả vòng đời kết nối, khác với REST xác thực từng request.

#### 3. Route `whoami` — giải pháp đúng bản chất thay vì bản vá

Bài toán tưởng nhỏ mà hoá ra là quyết định thiết kế quan trọng: Worker cần connectionId để push, client lại không tự biết connectionId của mình. Phương án đầu tiên nghĩ tới là để `$connect` handler push luôn một message "welcome" chứa connectionId — nhưng tài liệu và thực nghiệm cho thấy tại thời điểm `$connect` handler chạy, kết nối chưa chắc đã "sống" hoàn toàn, push ngay có rủi ro `GoneException` chập chờn khó tái hiện.

Giải pháp chọn: một route custom `whoami` — sau khi kết nối ổn định, client chủ động gửi `{"action": "whoami"}` và Lambda trả lại connectionId qua chính kết nối đó. Cách này biến thứ tự bất định ("server push lúc nào?") thành thứ tự xác định do client kiểm soát ("client hỏi khi nó sẵn sàng").

#### 4. Push lỗi không được làm hỏng cả batch

Lời gọi `PostToConnectionCommand` được bọc try/catch riêng, chỉ ghi warning khi thất bại (ví dụ client đã ngắt kết nối) — vì kết quả tóm tắt đã lưu an toàn trong DynamoDB, việc push chỉ là "thông báo", thất bại push không đồng nghĩa job thất bại. Nếu để lỗi push ném ra ngoài, message sẽ bị SQS retry và OpenAI bị gọi lại vô ích, tốn phí kép.

---

### Đánh giá kết quả tuần 11:

- Pipeline hoàn chỉnh với dữ liệu thật: Gmail → OpenAI → DynamoDB đã chạy ổn định, xác nhận bằng nhiều lần test.
- Toàn bộ hạ tầng WebSocket (API, Authorizer, 3 route, bảng mapping connection) đã khai báo xong trong SAM và deploy.
- Route `whoami` được thiết kế và triển khai như một quyết định kiến trúc có căn cứ, không phải bản vá — đã ghi rõ lý do vào tài liệu thiết kế để dùng cho phần bảo vệ báo cáo.
- Bàn giao format message WebSocket (`whoami-response`, `summary-ready`) cho thành viên Flutter, kèm hướng dẫn truyền JWT qua query string.

---

### Khó khăn gặp phải:

- Nhầm lẫn ban đầu về endpoint của Management API: cứ nghĩ push cũng dùng `wss://` như client kết nối, hoá ra backend phải gọi qua `https://` — sai protocol là lỗi ngay nhưng thông báo lỗi không nói rõ nguyên nhân.
- Lambda Authorizer cho WebSocket có cấu trúc event khác với Authorizer của REST API, copy code mẫu REST sang chạy sai âm thầm.
- Cân nhắc mất khá nhiều thời gian giữa hai phương án lấy connectionId (`$connect` push welcome vs route `whoami` riêng) — bài học là những quyết định "nhỏ" ở tầng giao thức thường tốn thời gian suy nghĩ hơn cả viết code.

---

### Hướng khắc phục và Best Practices đúc kết được:

- Với API Gateway WebSocket, ghi nhớ quy tắc: client kết nối bằng `wss://`, backend push bằng `https://` qua Management API — hai "mặt" khác nhau của cùng một API.
- Đọc kỹ cấu trúc event mẫu trong tài liệu cho từng loại Authorizer (REST vs WebSocket vs HTTP API) thay vì tái sử dụng code giữa các loại.
- Ghi lại lý do của mọi quyết định thiết kế ngay lúc quyết định (dù chỉ vài dòng) — một tuần sau sẽ không nhớ nổi vì sao chọn phương án này thay vì phương án kia.

---

### Định hướng cho tuần tiếp theo:

- Phối hợp với thành viên Flutter test end-to-end trên thiết bị thật: app kết nối WebSocket, gửi whoami, bấm Check Gmail và nhận kết quả push.
- Chuẩn bị tinh thần debug các vấn đề tích hợp — kinh nghiệm cho thấy phần ghép nối giữa các thành phần do nhiều người viết luôn phát sinh lỗi không lường trước.
- Rà soát lại toàn bộ kiến trúc, chuẩn bị số liệu chi phí và bảng tra cứu dịch vụ cho báo cáo.
