---
title: "Worklog Tuần 12"
date: 2026-06-22
weight: 12
chapter: false
pre: " <b> 1.12. </b> "
---

### Mục tiêu tuần 12: Tuần của những lỗi "vô hình" — debug tích hợp end-to-end

Backend đã xong từ tuần trước, app Flutter của thành viên nhóm cũng đã dựng xong — trên lý thuyết chỉ cần "cắm vào là chạy". Thực tế, tuần này trở thành tuần debug căng nhất của cả dự án: chuỗi lỗi nối tiếp nhau ở đúng những điểm ghép nối giữa các thành phần, mà từng thành phần riêng lẻ đều "có vẻ đúng". Với vai trò phụ trách backend và kiến trúc, tôi là người truy vết chính cho các lỗi xuyên tầng này.

- Hỗ trợ thành viên Flutter test end-to-end trên thiết bị Android thật, truy vết các lỗi tích hợp WebSocket.
- Giải quyết sự cố route `whoami` trả về `Forbidden` dù mọi resource đều báo tạo thành công.
- Truy vết và xử lý lỗi `410 GoneException` khi Worker push kết quả — bài toán connectionId "chết" mà không ai biết.
- Tối ưu Worker: chuyển xử lý email từ tuần tự sang song song, chịu lỗi từng phần tử.
- Tổng kết toàn bộ dịch vụ đã dùng, đối chiếu chi phí thực tế với Free Tier, hoàn thiện tài liệu kiến trúc cho báo cáo.

---

### Các công việc cần triển khai trong tuần này:

| Thứ | Hạng mục công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 2 | - Cùng thành viên Flutter chạy test end-to-end đầu tiên trên thiết bị thật. <br> - Ghi nhận hiện tượng: app báo "WebSocket chưa sẵn sàng", request `whoami` nhận về `{"message": "Forbidden"}`. | 22/06/2026 | 22/06/2026 | Nội bộ dự án |
| 3 | - Truy vết lỗi Forbidden: kiểm tra CloudWatch Logs của Lambda `ws-whoami`, phát hiện log group chưa từng tồn tại → request chưa bao giờ tới Lambda. <br> - Kiểm tra CloudFormation: mọi resource whoami đều `CREATE_COMPLETE`. Kiểm tra API Gateway Stages: phát hiện stage `prod` vẫn trỏ vào deployment cũ hơn ngày tạo route. | 23/06/2026 | 23/06/2026 | https://docs.aws.amazon.com/apigateway/ |
| 4 | - Deploy API thủ công vào stage `prod` để publish route mới, xác nhận whoami hoạt động. <br> - Nghiên cứu tài liệu: xác nhận `AWS::ApiGatewayV2::Deployment` không tự tạo bản mới khi route thay đổi, kể cả có `DependsOn` — ghi thành bài học cho báo cáo. | 24/06/2026 | 24/06/2026 | https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigatewayv2-deployment.html |
| 5 | - Sự cố mới: Check Gmail chạy nhưng app không nhận được kết quả. Log Worker báo `WebSocket push failed: GoneException (410)`. <br> - Bổ sung log chi tiết (`err.name`, `$metadata.httpStatusCode`) vào hàm push của Worker, deploy lại để thu thập dữ liệu chẩn đoán. | 25/06/2026 | 25/06/2026 | https://docs.aws.amazon.com/apigateway/ |
| 6 | - Đối chiếu timestamp giữa log `ws-disconnect` và log Worker: phát hiện connection đã đóng **trước** khi người dùng bấm nút — app đang gửi connectionId cũ đã chết. <br> - Cùng thành viên Flutter xác định nguyên nhân gốc ở tầng UI (state cache connectionId không đồng bộ với trạng thái kết nối thật) và phương án sửa (đọc giá trị tươi + tự reconnect). | 26/06/2026 | 26/06/2026 | Nội bộ dự án |
| 7 | - Tối ưu Worker: chuyển vòng lặp gọi OpenAI tuần tự sang `Promise.allSettled` — xử lý song song, một email lỗi không làm mất kết quả các email khác. <br> - Test lại end-to-end: kết quả tóm tắt hiển thị thành công trên app thật qua WebSocket push. | 27/06/2026 | 27/06/2026 | https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/allSettled |
| CN | - Tổng hợp bảng tra cứu dịch vụ (dịch vụ – vai trò – lý do chọn – rủi ro) cho toàn bộ kiến trúc. <br> - Đối chiếu Billing Dashboard, xác nhận chi phí nằm trong Free Tier + chi phí OpenAI ở mức thấp. <br> - Viết báo cáo tổng kết tuần và tài liệu bàn giao cho thành viên phụ trách viết docs. | 28/06/2026 | 28/06/2026 | Nội bộ dự án InboxIQ |

---

### Kết quả đạt được tuần 12:

#### 1. Bài học lớn nhất: "tạo thành công" không đồng nghĩa "đang chạy"

Sự cố route `whoami` trả `Forbidden` là bài học đắt giá nhất về CloudFormation và API Gateway. Mọi lớp kiểm tra thông thường đều báo ổn: `sam deploy` thành công, CloudFormation ghi nhận `CREATE_COMPLETE` cho cả 4 resource, route hiển thị đầy đủ trong Console. Nhưng stage `prod` vẫn đang chạy **deployment cũ** từ trước khi route tồn tại — vì `AWS::ApiGatewayV2::Deployment` chỉ tạo bản mới khi chính resource đó thay đổi thuộc tính, còn `DependsOn` chỉ đảm bảo thứ tự tạo, không ép re-deploy.

Kỹ thuật truy vết then chốt: kiểm tra **log group của Lambda đích có tồn tại không**. Log group chỉ được tạo khi Lambda chạy lần đầu — "log group does not exist" là bằng chứng tuyệt đối rằng request chưa từng chạm tới hàm, khoanh vùng lỗi ngay về tầng routing thay vì mất thời gian nghi ngờ code.

#### 2. Truy vết lỗi 410 Gone bằng đối chiếu timestamp — debug như điều tra

Lỗi thứ hai tinh vi hơn nhiều vì hoàn toàn "âm thầm": người dùng bấm nút, mọi API trả về thành công, nhưng kết quả không bao giờ hiện ra. Log Worker cho thấy push thất bại với `410 GoneException` — connection không còn tồn tại. Câu hỏi là: nó chết lúc nào, và tại sao app vẫn dùng nó?

Phương pháp giải: đặt log của ba nguồn (ws-disconnect, thời điểm bấm nút suy từ jobId, log Worker) lên cùng một trục thời gian. Kết quả rõ như ban ngày — connection đã đóng 18 giây **trước** khi người dùng bấm nút. Vấn đề không nằm ở backend: app đang giữ một connectionId cũ trong state của màn hình, không đồng bộ khi kết nối thật đã rớt. Từ chẩn đoán này, thành viên Flutter sửa đúng chỗ (đọc connectionId "tươi" từ service tại thời điểm dùng, tự reconnect nếu null) thay vì sửa mò.

Bài học phương pháp luận: với hệ bất đồng bộ nhiều thành phần, **timestamp là công cụ chẩn đoán mạnh nhất** — nhiều lỗi chỉ hiện nguyên hình khi xếp các sự kiện lên cùng một dòng thời gian.

#### 3. `Promise.allSettled` — chịu lỗi từng phần tử thay vì "được ăn cả ngã về không"

Phiên bản đầu của Worker gọi OpenAI tuần tự cho từng email — thời gian tăng tuyến tính theo số email và một email lỗi làm hỏng cả batch. Chuyển sang `Promise.allSettled`: các email xử lý song song (tổng thời gian ≈ email chậm nhất thay vì tổng cộng dồn), và email nào lỗi thì bị loại riêng, các email thành công vẫn trả kết quả bình thường. Khác biệt với `Promise.all` (reject cả cụm khi một phần tử lỗi) là chi tiết quan trọng cần nói rõ khi bảo vệ báo cáo.

#### 4. Hệ thống hoàn chỉnh end-to-end trên thiết bị thật

Cuối tuần, chuỗi đầy đủ đã được kiểm chứng: người dùng bấm Check Gmail trên app Android thật → Producer → SQS → Worker (Gmail + OpenAI song song) → DynamoDB → push WebSocket → danh sách tóm tắt hiện trên màn hình trong vài giây. Chi phí toàn bộ quá trình phát triển vẫn nằm trong Free Tier của AWS, cộng chi phí OpenAI không đáng kể.

---

### Đánh giá kết quả tuần 12:

- Giải quyết triệt để hai lỗi tích hợp khó nhất dự án (route chưa publish, connectionId chết) bằng phương pháp truy vết có hệ thống thay vì thử-sai.
- Worker được tối ưu về cả tốc độ (song song) lẫn độ bền (chịu lỗi từng phần tử).
- Hệ thống chạy hoàn chỉnh end-to-end trên thiết bị thật — mục tiêu kỹ thuật chính của cả dự án nhóm đã đạt.
- Hoàn thành bảng tra cứu dịch vụ và số liệu chi phí, bàn giao cho thành viên phụ trách tài liệu để đưa vào báo cáo chung.

---

### Khó khăn gặp phải:

- Cả hai lỗi lớn của tuần đều "vô hình" theo nghĩa đen: không có thông báo lỗi nào hiện ra cho người dùng, mọi thành phần riêng lẻ đều báo thành công — chỉ có kết quả cuối cùng là không xuất hiện.
- Thông báo lỗi của API Gateway (`Forbidden`) và AWS SDK (`UnknownError`) quá chung chung, không chỉ thẳng nguyên nhân, buộc phải suy luận từ bằng chứng gián tiếp (log group tồn tại hay không, mã HTTP trong `$metadata`).
- Debug lỗi xuyên tầng đòi hỏi phối hợp chặt với thành viên Flutter — có lúc mỗi bên đều tin phần mình đúng, phải cùng ngồi đối chiếu log mới tìm ra điểm ghép bị lệch.

---

### Hướng khắc phục và Best Practices đúc kết được:

- Sau mỗi lần thêm/sửa route trên API Gateway quản lý bằng CloudFormation, luôn kiểm tra Deployment history của stage — đừng tin "deploy thành công" của công cụ.
- Luôn log đầy đủ `err.name` và `$metadata.httpStatusCode` khi bắt lỗi AWS SDK — `err.message` đơn thuần thường vô dụng với lỗi hạ tầng.
- Khi debug hệ bất đồng bộ, việc đầu tiên là dựng dòng thời gian từ log của mọi thành phần liên quan, trước khi đưa ra bất kỳ giả thuyết nào.
- Trong hệ thống nhiều người viết, lỗi thường nằm ở "đường ghép" giữa các phần chứ không nằm trong phần của ai — phân công debug nên theo luồng dữ liệu, không theo ranh giới sở hữu code.

---

### Định hướng sau dự án:

- Bổ sung `WidgetsBindingObserver` phía Flutter để tự reconnect WebSocket khi app quay lại từ nền (hiện chỉ reconnect khi bấm nút) — đã ghi vào danh sách bảo trì.
- Cân nhắc cơ chế ép API Gateway deployment tự làm mới khi route thay đổi (gắn hash vào logical ID của Deployment) để lỗi "route chưa publish" không tái diễn.
- Nâng cấp Lambda runtime khỏi Node.js 20.x (đã EOL) trước các mốc ảnh hưởng thực tế năm 2027.
- Chuẩn bị nội dung thuyết trình phần kiến trúc và các quyết định thiết kế cho buổi bảo vệ báo cáo nhóm.
