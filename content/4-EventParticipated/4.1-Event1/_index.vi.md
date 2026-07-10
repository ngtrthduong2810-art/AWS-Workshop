---
title: "Event 1"
date: 2026-05-09
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

# Bài thu hoạch "FCAJ Community Day"

### Mục Đích Của Sự Kiện

- Giới thiệu các cơ chế khoa học thần kinh (đặc biệt là cách vận hành của Dopamine) giúp người học xây dựng động lực và giữ vững kỷ luật trên hành trình tự học.
- Trang bị kỹ thuật thiết kế Prompt ở mức nâng cao (Ultimate Prompt Engineering) nhằm khai thác tối đa hiệu quả khi làm việc cùng các mô hình ngôn ngữ lớn.
- Cung cấp góc nhìn thực tế về con đường sự nghiệp và những tiêu chí mà doanh nghiệp thật sự dùng để đánh giá ứng viên, dành riêng cho sinh viên CNTT năm 3, năm 4.
- Trình bày phương pháp phát triển phần mềm BMX (BMM method) — cách tổ chức AI Agent theo quy trình bài bản để hạn chế tối đa hiện tượng ảo tưởng (hallucination).

### Danh Sách Diễn Giả

- **Anh Long** - Chuyên gia chia sẻ về Kỹ thuật Hack não bộ
- **Anh Thịnh** - Ultimate Prompt Engineering.
- **Anh Khang** - Solutions Architect tại Cloud Kinetics (Hơn 3 năm kinh nghiệm tuyển dụng và định hướng kỹ sư công nghệ).
- **Chị Thảo** - Software Developer tại Ngân hàng Quốc tế Việt Nam (VIB).

### Nội Dung Nổi Bật

#### Phương pháp "Hack não bộ" để nghiện học như nghiện Game/Mạng xã hội

- **Cơ chế Dopamine**: Điều thú vị là Dopamine không xuất hiện vào lúc ta nhận được phần thưởng — nó bùng lên mạnh nhất khi não bộ đang _mong chờ phần thưởng sắp tới_. Đây chính là "công thức bí mật" mà các nền tảng như TikTok khai thác: người dùng bị giữ chân bởi cảm giác tò mò không biết nội dung kế tiếp là gì.
- **Áp dụng vào học tập qua 4 cơ chế**: Tò mò → Thử nghiệm → Khám phá → Thỏa mãn.
- **Các kỹ thuật cốt lõi**:
- _Tâm lý sợ mất chuỗi (Loss Aversion)_: Dùng một cuốn lịch treo tường hoặc ứng dụng đếm chuỗi để ghi lại số ngày học liên tiếp (tương tự streak của Duolingo hay TikTok). Cảm giác tiếc nuối khi sắp đánh mất một chuỗi dài sẽ trở thành động lực buộc bản thân ngồi vào bàn học, dù chỉ 5–10 phút.
- _Đánh lừa hạch hạnh nhân (Amygdala)_: Trước một núi kiến thức, phản xạ tự nhiên của não là sợ hãi và né tránh. Giải pháp là băm nhỏ mục tiêu — thay vì ép mình học AWS liền 5 tiếng, chỉ cần tập trung vào một dịch vụ duy nhất trong 10-20 phút.
- _Quy tắc 2 phút_: Bất cứ việc gì hoàn thành được trong vòng 2 phút (mở file bài tập ra, đọc một trang tài liệu) thì bắt tay làm ngay — đây là cách phá vỡ vòng lặp trì hoãn hiệu quả nhất.
- _Hệ thống Phản hồi & Gamification_: Tự "game hoá" việc học của chính mình: thiết kế thang điểm kinh nghiệm (XP), hệ thống thăng hạng (Đồng, Bạc, Vàng, Cam theo mô hình rank của FCJ) và chuẩn bị sẵn các hộp quà bốc thăm ngẫu nhiên sau mỗi phiên học để nuôi dưỡng Dopamine đều đặn.

#### Kỹ thuật Kỹ nghệ Prompt Nâng cao (Ultimate Prompt Engineering)

- **7 thành phần của một Prompt chuẩn chỉnh**: Role (Vai trò), Instruction (Chỉ thị), Context (Bối cảnh), Input Data (Dữ liệu đầu vào), Output Format (Định dạng đầu ra), Examples (Ví dụ minh họa), và Constraints (Ràng buộc).
- **Tối ưu hóa Token**: LLM không đọc từng chữ mà xử lý theo các cụm từ phụ (subwords) gọi là token. Một điểm đáng lưu tâm cho doanh nghiệp Việt: cùng một nội dung, văn bản tiếng Việt khi đi qua bộ mã hóa (Tokenizer) thường "ngốn" số token gấp đôi so với tiếng Anh — đồng nghĩa hóa đơn API cũng tăng theo tương ứng.
- **Kỹ thuật tư duy nâng cao**:
- _Chain of Thought (CoT)_: Yêu cầu AI trình bày lập luận theo từng bước tuần tự, nhờ đó độ chính xác của kết quả được cải thiện rõ rệt.
- _Tree of Thought (ToT)_: Tổ chức quá trình suy luận thành cấu trúc cây, kết hợp các thuật toán duyệt DFS/BFS để mô hình tự so sánh nhiều nhánh giải pháp và chọn ra hướng đi tối ưu.
- _Self-Consistency_: Cho mô hình chạy nhiều luồng suy luận độc lập song song, sau đó chốt đáp án theo nguyên tắc đa số.

- **Case Study (Project Prompt Optimizer)**: Một dự án tối ưu hóa prompt tự động vận hành trọn vẹn trên nền tảng Serverless của AWS: CloudFront + S3 đảm nhiệm Frontend/CDN, Amazon Cognito quản lý người dùng và JWT, bộ đôi API Gateway + AWS Lambda điều phối traffic và xử lý logic, DynamoDB lưu lịch sử prompt với độ trễ truy vấn tính bằng mili-giây, và Amazon Bedrock làm cầu nối bảo mật tới các Foundation Model như Claude 3.5 Sonnet.

#### Định hướng nghề nghiệp dành cho sinh viên ("Tại sao các bạn chưa đi làm?")

- **Hiệu ứng Khuếch đại của AI (AI Amplification)**: AI hoạt động như một chiếc loa phóng đại — người lười biếng, hời hợt sẽ càng tệ đi (copy-paste code máy sinh ra mà không hiểu gì), trong khi người có nền tảng vững sẽ nhân đôi, nhân mười năng suất. Thực tế tuyển dụng: doanh nghiệp thà chọn ứng viên 6-7 điểm nhưng tư duy bằng chính đầu óc mình, còn hơn một bài nộp 9-10 điểm do AI làm hộ mà khi hỏi lại thì ú ớ không giải thích nổi.
- **Tư duy "Why" thay vì "What"**: Đừng dừng ở câu hỏi "làm sao cho xong bài" (What) — hãy tự chất vấn "Vì sao lại chọn kiến trúc/dịch vụ này?", "Đánh đổi (trade-off) ở đây là gì?". Lặp lại câu hỏi "Why" tối thiểu 5 lần là cách đào tới tận gốc rễ của mọi vấn đề.
- **Sự liêm chính (Integrity) & Tầm nhìn dài hạn**: Người làm việc có liêm chính khi nhận 10 yêu cầu sẽ tự mình bóc tách thêm 20-30 trường hợp ngoại lệ (Edge cases) để xử lý cho trọn vẹn — làm việc tử tế cả khi không ai giám sát. Với người mới ra trường, hãy ưu tiên tích lũy trải nghiệm dài hạn thay vì bị cuốn theo con số lương khởi điểm.
- **Mô hình 3 vòng tròn công việc & 5 lợi ích**: Công việc lý tưởng nằm ở giao điểm của ba vòng tròn: điều bạn yêu thích, điều doanh nghiệp yêu cầu phải làm đúng chuẩn, và lợi ích bạn thu về. Một công việc mang lại 5 giá trị: Lương (Salary), Kinh nghiệm (Experience), Mạng lưới quan hệ (Network), Kiến thức (Knowledge) và Cơ hội thăng tiến (Promotion).
- **Bộ 5 tiêu chí đánh giá ứng viên của doanh nghiệp**: Thái độ (Attitude — yếu tố xếp số 1 với Fresher), Trình độ/Học vấn (Education), Kinh nghiệm (Experience), Trải nghiệm thực tế (Exposure), và Tố chất bản năng (Talents).

#### Phương pháp phát triển phần mềm BMX (BMM Method) kết hợp AI Agent

- **Khái niệm**: BMX (Through Method for Agile Development) là phương pháp mã nguồn mở đưa quy trình làm việc với AI vào khuôn khổ Agile truyền thống: hệ thống được vận hành bởi các AI Agent đảm nhận từng vai trò độc lập — PM, Architect, PO, Scrum Master, Developer, Reviewer/QA.
- **Giảm thiểu ảo tưởng (Hallucination)**: Khi dồn tất cả yêu cầu vào một khung chat duy nhất, Context Window phình to quá mức khiến AI rối loạn và sinh code sai. BMX hóa giải vấn đề này bằng cách chẻ nhỏ tài liệu PRD (Product Requirement Document) và System Architecture thành từng Epic, từng Story gọn gàng và độc lập với nhau.
- **Cơ chế hoạt động**: Mỗi Story đi qua chuỗi trạng thái do con người kiểm soát nghiêm ngặt (Draft → Approved → Review → Done). Developer Agent chỉ được phép nhận và triển khai những Story đã qua phê duyệt (Approved); tiếp đó Reviewer Agent cùng QA Agent chạy vòng lặp kiểm thử liên tục cho tới khi tỷ lệ lỗi về 0. Triết lý cốt lõi của phương pháp: đừng quản lý mã nguồn — hãy viết Document thật chuẩn chỉnh, phần sinh code tốt nhất cứ để AI lo.

### Những Gì Học Được

#### Tư Duy Thiết Kế

- **Tư duy hướng bản chất (Foundation-first approach)**: Không cần ôm đồm chinh phục cả 200–300 dịch vụ trong hệ sinh thái AWS — nắm thật chắc, thật sâu 5 dịch vụ nền tảng cốt lõi đã đủ làm bàn đạp để thiết kế kiến trúc cho hầu hết bài toán.
- **Tư duy phản biện kiến trúc**: Duy trì một quy trình tư duy (Thought process) chất vấn liên tục bằng câu hỏi "Why" khi làm việc với AI — không dễ dãi chấp nhận câu trả lời đầu tiên, để không rơi vào bẫy ảo tưởng của mô hình ngôn ngữ lớn.

#### Kiến Trúc Kỹ Thuật

- Nắm vững **7 thành phần cấu trúc Prompt chuyên sâu** và biết cách vận dụng vào công việc thường nhật để nâng chất lượng phản hồi nhận về từ AI.
- Hiểu bản chất chi phí khi vận hành hệ thống LLM thông qua **cơ chế tính Token** — đặc biệt là khoảng chênh lệch gấp đôi giữa xử lý tiếng Việt so với tiếng Anh.
- Hình dung rõ cách **điều phối nhiều AI Agent** theo mô hình BMX: chia module, đóng gói Context Window riêng cho từng Agent chuyên trách, đảm bảo mỗi nhiệm vụ được thực thi độc lập mà không gây tác động chéo lên các tính năng khác.

#### Chiến Lược Hiện Đại Hóa

- **Chiến lược phát triển dựa trên tài liệu (Document-driven)**: Dịch chuyển trọng tâm từ "ngồi viết code" sang "viết tài liệu kỹ thuật chuẩn chỉnh" — để năng lực sinh code tự động của AI Agent được phát huy tối đa.
- **Chiến lược tích lũy trải nghiệm dài hạn**: Học cách đón nhận sai lầm như một phần tất yếu (Embrace mistakes) và nhìn sự nghiệp bằng lăng kính dài hạn (Long-term vision), thay vì chỉ chăm chăm vào các mục tiêu tài chính trước mắt.

### Ứng Dụng Vào Công Việc

- **Tái cấu trúc quy trình Prompt hàng ngày**: Đưa trọn bộ 7 thành phần cấu trúc (Role, Instruction, Context, Constraints...) vào workflow làm việc với Gemini/ChatGPT để cải thiện rõ rệt chất lượng đầu ra.
- **Áp dụng tư duy "Why" vào dự án hiện tại**: Chủ động tự đặt ra và giải quyết thêm các trường hợp ngoại lệ (Edge cases) cho những tính năng đang phát triển — một cách rèn luyện tính liêm chính (Integrity) qua công việc thực tế.
- **Xây dựng chuỗi kỷ luật tự học**: Kết hợp phương pháp gạch lịch/tích chuỗi (Loss Aversion) với quy tắc 2 phút để giữ thói quen học công nghệ mới (các dịch vụ như AWS Lambda, Bedrock) đều đặn tối thiểu 15-30 phút mỗi ngày.
- **Nghiên cứu phương pháp BMX**: Tải và thử nghiệm BMX từ GitHub vào các project cá nhân hoặc project nhóm, đánh giá hiệu quả của việc phân tách tác vụ và quản lý mã nguồn bằng AI Agent.
- **Thúc đẩy kỹ năng collab nhóm**: Mạnh dạn tham gia chia sẻ tại các buổi Tech Meetup cộng đồng — vừa rèn kỹ năng thuyết trình, phản biện, vừa mở rộng mạng lưới quan hệ (Network).

### Trải nghiệm trong event

Được góp mặt tại workshop **"FCAJ Community Day"** là một trải nghiệm thực sự đáng giá với tôi: sự kiện vừa mở rộng tầm nhìn kỹ thuật (Prompt nâng cao, AI Agents, Serverless), vừa mang đến những bài học định hướng nghề nghiệp rất "đời" từ những người đi trước. Một vài dấu ấn đáng nhớ:

#### Học hỏi từ các diễn giả có chuyên môn cao

- Những chia sẻ thẳng thắn, không tô vẽ của anh Khang (Cloud Kinetics) và chị Thảo (VIB) về môi trường doanh nghiệp thực tế đã giúp tôi gỡ bỏ nhiều ngộ nhận — về giá trị thật của điểm số, và về hậu quả của việc phụ thuộc AI khi làm bài test tuyển dụng.

#### Trải nghiệm kỹ thuật thực tế

- Được tận mắt xem demo kiến trúc Serverless của dự án Prompt Optimizer với sự góp mặt của Amazon Bedrock, DynamoDB và Lambda.
- Lần đầu tiếp cận các khái niệm prompt engineering nâng cao như Tree of Thought (ToT) và Chain of Thought (CoT) qua những sơ đồ tư duy trình bày từng bước rất trực quan.
- Nắm được cách một hệ sinh thái AI Agent vận hành bài bản qua lăng kính phương pháp BMX — từ khâu Planning cho tới Review/QA, mỗi vai trò được phân tách một cách khoa học.

#### Ứng dụng công cụ hiện đại

- Học được cách đứng ở vị thế người làm chủ công cụ AI để nhân năng suất, thay vì trở thành nạn nhân của hiệu ứng khuếch đại (AI Amplification). Biết tận dụng AI hết công suất cho việc brainstorm và phát triển ý tưởng, nhưng phần tư duy cốt lõi vẫn luôn nằm trong tay mình.

#### Kết nối và trao đổi

- Không khí sự kiện cởi mở và giàu tính kết nối, khuyến khích sinh viên chủ động đặt câu hỏi, phản biện không e dè. Workshop tiếp cho tôi nguồn động lực lớn để tự tin chia sẻ kiến thức với cộng đồng mà không sợ nói sai — bởi "sai lầm là một phần của hành trình tích lũy trải nghiệm".

#### Bài học rút ra

- Người về đích trên hành trình phát triển bản thân không phải người thông minh nhất, mà là người bền bỉ nhất và biết tự kiến tạo cho mình một môi trường học tập tốt.
- AI không thay thế lập trình viên — nhưng lập trình viên hiểu bản chất vấn đề và làm chủ được công cụ AI (prompt nâng cao, mô hình AI Agent) sẽ thay thế những người không làm được điều đó.
- Giữ vững sự liêm chính trong mọi việc mình làm, đặt câu hỏi "Why" cho từng quyết định kỹ thuật, và luôn nhìn con đường sự nghiệp bằng tầm nhìn dài hạn.

#### Một số hình ảnh khi tham gia sự kiện

- ![Ảnh minh chứng: tham gia event](</images/4-EventParticipated/Event1/event1(0).jpg>)
- ![Ảnh minh chứng: tham gia event](</images/4-EventParticipated/Event1/evt1(1).jpg>)
  > Nhìn lại toàn bộ sự kiện, giá trị nhận được không chỉ dừng ở khối kiến thức kỹ thuật chuyên sâu về Prompt Engineering hay mô hình phát triển phần mềm trong kỷ nguyên AI — điều đọng lại lớn hơn cả là ngọn lửa đam mê, tinh thần kỷ luật tự học và một tư duy nghề nghiệp đúng đắn được truyền lại cho thế hệ kỹ sư công nghệ kế tiếp.
