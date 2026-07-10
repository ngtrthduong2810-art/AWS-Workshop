---
title: "Event 2"
date: 2026-05-23
weight: 2
chapter: false
pre: " <b> 4.2. </b> "
---

# Bài thu hoạch "FCAJ Community Day - May 2026 Edition"

### Mục Đích Của Sự Kiện

- Mang đến bức tranh vĩ mô mới nhất về thị trường CNTT Việt Nam giữa bối cảnh AI đang phát triển với tốc độ chóng mặt.
- Đào sâu phương pháp tổ chức cấu trúc Prompt để tối ưu hóa ngữ cảnh (Context Optimization) và làm chủ tính ngẫu nhiên (Randomness) vốn có của LLM.
- Trình diễn giải pháp trợ lý phân tích dữ liệu doanh nghiệp dựa trên Amazon Q Business (QuickSight/Q Desktop) kết hợp với MCP server.
- Kể lại hành trình thực chiến tại cuộc thi Hackathon và cách xây dựng hệ thống Multi-Agent đạt chuẩn Enterprise cho lĩnh vực tài chính - ngân hàng.

### Danh Sách Diễn Giả

- **Anh Nguyễn Gia Hưng** - Solutions Architect tại AWS Việt Nam & Founder của FCAJ (Chia sẻ về định hướng vĩ mô thị trường).
- **Anh Tịnh Trương** - Platform Engineer tại Gothamic X (Chia sẻ về Kỹ thuật tối ưu hóa ngữ cảnh và Randomness của LLM).
- **Anh Hải Anh** - Solutions Architect tại Pacific Việt Nam (Chia sẻ về Amazon Q Business & MCP).
- **Anh Nguyễn Hấn Thịnh** - DevOps Engineer (Chia sẻ về cơ chế Flat-rate Pricing và bảo mật nâng cao của Amazon CloudFront).
- **Bạn Uyển, Bạn Mách & Chị Thảo** - Nhóm Winner Hackathon (Chia sẻ về hành trình 36 giờ phát triển dự án UTMorpho).
- **Diễn giả cuối (Kỹ sư FinTech)** - Cố vấn giải pháp FinTech tại VPBank (Chia sẻ về kiến trúc Multi-Agent ứng dụng trong ngân hàng).

### Nội Dung Nổi Bật

#### 1. Định vị thị trường CNTT và Cơ hội nghề nghiệp mới trong thời đại AI

- **Nghịch lý "Đèn LED" và sự bùng nổ phần mềm**: Lịch sử bóng đèn LED cho một bài học bất ngờ — khi chi phí chiếu sáng giảm còn 1/10, người ta không thắp sáng ít đi mà thắp sáng nhiều gấp bội. Phần mềm cũng vậy: AI khiến việc viết mã trở nên rẻ chưa từng có, và hệ quả là nhu cầu phát triển phần mềm toàn cầu sẽ không co lại mà bùng nổ dữ dội. Bằng chứng sống động: ngay cả những người ngoài ngành IT (luật sư, bác sĩ) giờ đây đã có thể giành giải tại các Hackathon lớn của Anthropic.
- **Luồng gió công việc mới - Fix Code rác & Platform Engineering**: Khi ai cũng sinh được code bằng AI, thị trường sẽ ngập trong các sản phẩm MVP/đồ án đầy lỗi hoặc chạy chập chờn không thể vận hành ổn định. Chính điều đó mở ra hai luồng nhu cầu tuyển dụng tăng mạnh trong dài hạn: kỹ sư chuyên "dọn dẹp code rác" và cải tiến hệ thống, cùng đội ngũ Platform Engineering xây dựng nền tảng tự động hóa hạ tầng (IDP - Internal Developer Platform) cho các tổ chức quy mô lớn.
- **Thực tế tuyển dụng tại Việt Nam**: Các tập đoàn công nghệ toàn cầu vẫn đều đặn mở Technical Hub tại Việt Nam để săn đón nhân tài bản địa. Bài toán đặt ra cho kỹ sư Việt: đầu tư vào sự tự tin, năng lực tiếng Anh, hiểu biết nghiệp vụ thực tế (Domain knowledge) và khả năng làm ra sản phẩm chạy được thật (Production-ready) — thay vì mãi dừng lại ở những bài demo nhỏ lẻ.

#### 2. Kỹ thuật tối ưu hóa ngữ cảnh và Kiểm soát tính ngẫu nhiên (Randomness) của LLM

- **Lỗi đổi Context liên tục**: Thói quen tai hại mà rất nhiều người mắc phải: dồn đủ thứ chủ đề vào chung một phiên chat — từ hỏi lịch du lịch, nhờ sửa CV cho đến viết code. Context Window vì thế bị xáo trộn liên tục, và AI trượt vào trạng thái "ảo tưởng" (hallucination) nhanh hơn hẳn.
- **Cơ chế Temperature và điểm số Logit**: Về bản chất, LLM là một "probabilistic engine" — nó chấm điểm (logit) cho từng từ ứng viên có thể xuất hiện tiếp theo rồi lựa chọn dựa trên xác suất. Khi kéo `Temperature = 0`, cơ chế chọn từ chuyển từ Softmax sang Argmax — luôn luôn lấy từ có điểm cao nhất — nhờ đó câu trả lời trở nên định tính và nhất quán (consistent) qua các lần chạy.
- **Sự khác biệt giữa API Cloud và Local Host**: Một sự thật ít người biết: kể cả khi đã đặt `Temperature = 0`, gọi API của OpenAI hay Amazon Bedrock nhiều lần vẫn có thể nhận về kết quả khác nhau. Hai thủ phạm đứng sau: phép tính song song trên GPU gây lệch số thập phân khi làm tròn, và các kỹ thuật tối ưu thương mại (Inference Optimization) của nhà cung cấp — gộp nhiều prompt ngắn của nhiều người dùng vào cùng một lượt xử lý để tiết kiệm chi phí. Muốn kiểm soát độ nhất quán tuyệt đối 100%, con đường duy nhất là tự host model trên hạ tầng Local.

#### 3. Hệ sinh thái Amazon Q Business & Trợ lý phân tích dữ liệu thế hệ mới

- **Xây dựng cánh tay nối dài bằng MCP (Model Context Protocol)**: AI Agent thời nay không thể chỉ dừng ở việc trả lời bằng văn bản — nó phải hành động được (Action). Thông qua các cổng MCP, Agent có thể trực tiếp đặt lịch họp, tự động gửi mail, hay kết nối thẳng vào hệ thống Jira, Confluence, Microsoft Cloud, Google Suite của doanh nghiệp.
- **Trợ lý phân tích dữ liệu tự động**: Với Amazon Q Business (hoặc QuickSight Desktop), một nhân viên doanh nghiệp không hề biết gì về BI (Business Intelligence) chỉ cần thả file Excel dữ liệu thô vào — hệ thống lập tức tự phân tích và dựng lên một Dashboard trực quan hoàn chỉnh trong thời gian ngắn đáng kinh ngạc.

#### 4. Case Study: Dự án UTMorpho thắng giải Hackathon trong 36 giờ liên tục

- **Ý tưởng giải quyết nỗi đau thực tế (Pain point)**: Nhóm không chạy theo những ý tưởng vĩ mô hào nhoáng mà nhắm thẳng vào một nỗi đau rất cụ thể của lập trình viên: mỗi khi muốn sửa một chi tiết nhỏ trên giao diện do AI sinh ra, họ buộc phải yêu cầu AI gen lại toàn bộ từ đầu — vừa mất thời gian vừa đốt Token.
- **Kiến trúc Multi-Agent của UTMorpho**: Dự án chạy trên mô hình Serverless của AWS với 3 Agent chuyên biệt phối hợp nhịp nhàng:
  - *Agent 1 (Vision Agent)*: Tiếp nhận hình ảnh/bản phác thảo từ camera người dùng, bóc tách nội dung thành file cấu trúc JSON.
  - *Agent 2 (Layout Agent)*: Đọc file JSON và tính toán cấu trúc CSS, bố cục layout cùng kích thước các thành phần.
  - *Agent 3 (Design Agent)*: Nhận đầu ra của Agent 2, biên dịch thành mã HTML/CSS hoàn chỉnh và hiển thị theo thời gian thực (Streaming UI).
- **Tính năng nổi bật**: Trang bị một trình Editor trực quan cho phép lập trình viên kéo thả, di chuyển vị trí component ngay trên giao diện đang hiển thị, đồng thời xuất link HTML public để chia sẻ cho đồng nghiệp cùng review.

#### 5. Kiến trúc Multi-Agent chuẩn Enterprise cho nghiệp vụ Ngân hàng (VPBank Practice)

- **Bài toán Nghiệp vụ - Đánh giá tín dụng cho Startup**: Quy trình duyệt vay truyền thống đòi hỏi báo cáo tài chính 3 năm liên tiếp cùng tài sản thế chấp vật lý — một cánh cửa gần như đóng sập với các Startup vốn chỉ sở hữu tài sản trí tuệ và mới hoạt động được 3-6 tháng. Lời giải được đề xuất: một hệ thống Multi-Agent phân tích đa chiều dựa trên các nguồn dữ liệu phi truyền thống.
- **Thiết kế Hệ thống Multi-Agent chuyên biệt**:
  - *Credit Committee Agent (Manager/Orchestrator)*: Giữ ghế chủ tọa hội đồng — phân phối nhiệm vụ cho các Agent thành viên và tổng hợp bản báo cáo cuối cùng.
  - *Financial Analyst Agent*: Chuyên trách phân tích sâu báo cáo tài chính ngắn hạn và dòng tiền của doanh nghiệp.
  - *Market Research Agent*: Đánh giá thị phần (Tam, Sam, Som), đối thủ cạnh tranh và các xu hướng thị trường liên quan.
  - *Team Evaluator Agent*: Thu thập dữ liệu và thẩm định năng lực đội ngũ Founders qua hồ sơ công nghệ cùng dấu chân trên Twitter(X), LinkedIn, Facebook.
  - *Risk Assessor Agent*: Gánh vai trò then chốt nhất — giám sát ranh giới hoạt động của mọi Agent còn lại, lọc dữ liệu hai chiều (Input/Output filtering) nhằm chống rò rỉ thông tin mật và chặn đứng các đòn tấn công Prompt Injection, tuân thủ tiêu chuẩn nghiêm ngặt của Ngân hàng Nhà nước.

### Những Gì Học Được

#### Tư Duy Thiết Kế

- **Tư duy hướng nghiệp vụ thực tế (Business-Driven Mindset)**: Mọi giải pháp công nghệ trong doanh nghiệp lớn đều phải vượt qua bài kiểm tra 4 câu hỏi trước khi bắt tay thiết kế: Ai xài? Xài cái gì? Tại sao người ta phải xài? Khi nào là thời điểm thích hợp để triển khai?
- **Tư duy phân tách trách nhiệm (Separation of Concerns)**: Mỗi AI Agent chỉ nên gánh đúng một vai trò chuyên môn, được định hình rõ ràng qua Backstory và System Prompt riêng — vừa tránh làm quá tải Context Window, vừa giúp mô hình phân phối sự chú ý (Attention) hiệu quả nhất.

#### Kiến Trúc Kỹ Thuật

- Làm chủ **Cơ chế kiểm soát tính định tính (Determinism)** của LLM thông qua bộ tham số `Temperature`, `Top P`, và `Repeat Penalty` — điều chỉnh linh hoạt tùy theo đầu ra cần sáng tạo (văn bản) hay cần chính xác tuyệt đối (JSON/Code).
- Hiểu sâu về hạ tầng mạng nội bộ **AWS Backbone & PoP (Points of Presence)** đứng sau CloudFront: cách CDN gộp request theo nhiều tầng để che chắn Origin Server trước các đợt tấn công volumetric DDoS hay Syn Flush nhờ tính năng Syn Proxy.
- Nhận thức rõ giá trị của quản lý hạ tầng bằng mã nguồn với **Terraform (Infrastructure as Code)**: kiểm soát phiên bản tài nguyên và tái lập (Reproduce) toàn bộ hệ thống trên nhiều Region khác nhau của AWS.

#### Chiến Lược Hiện Đại Hóa

- **Chiến lược đo lường ROI (Return on Investment)**: Muốn ban lãnh đạo Enterprise gật đầu với một dự án AI, phải nói chuyện bằng những con số cụ thể (Numbers speak louder than words) — chu kỳ hoàn vốn (Payback period) là bao lâu, mỗi năm tiết kiệm cho doanh nghiệp bao nhiêu tiền — chứ không phải chỉ trình một bản demo công nghệ đẹp mắt.
- **Chiến lược kiểm thử liên tục (Testing, Testing, Testing)**: Con đường đưa một hệ thống AI đạt chuẩn Production trong môi trường khắt khe là các bài test động, test sâu xuống tận tầng downstream services — đảm bảo hệ thống đứng vững trong mọi kịch bản AI sinh sai format.

### Ứng Dụng Vào Công Việc

- **Cấu hình tham số Temperature mindful hơn**: Chủ động đặt `Temperature = 0` hoặc `0.1` mỗi khi cần AI sinh định dạng có cấu trúc chặt như JSON/HTML trong dự án hiện tại — giảm hẳn tỷ lệ lỗi lệch dấu ngoặc, dấu phẩy.
- **Áp dụng kiến trúc Multi-Agent phòng ngừa lỗi**: Không dồn cả quy trình vào một khung chat duy nhất nữa — bài toán sẽ được chẻ thành các sub-agents hoạt động độc lập (học theo mô hình UTMorpho), kèm một Agent quản lý đứng trên kiểm tra chéo kết quả.
- **Nâng cao tính bảo mật cho ứng dụng**: Dựng các lớp lọc dữ liệu nhạy cảm (Input/Output filtering) bằng AWS Lambda ngay trước cửa ngõ truyền dữ liệu vào các mô hình ngôn ngữ lớn, đáp ứng quy định bảo mật nội bộ của tổ chức.
- **Chuyển đổi sang quản lý hạ tầng bằng Terraform**: Khởi động việc viết Terraform cho các dịch vụ CloudFront, S3 của hệ thống, dần thay thế lối cấu hình thủ công (Click engineering) trên Console — vừa dễ quản lý phiên bản, vừa thuận tiện rotate API Keys/Access Keys theo định kỳ.
- **Tập trung vào kiến thức Backend nền tảng**: Kiên trì rèn tư duy kỹ nghệ phần mềm cốt lõi (Software Engineering), nắm chắc cấu trúc dữ liệu và API contract — bởi AI chỉ là công cụ giúp xây sản phẩm nhanh hơn, còn tư duy hệ thống của người kỹ sư mới là yếu tố quyết định sau cùng.

### Trải nghiệm trong event

Tham dự workshop **"FCAJ Community Day"** lần này với tôi là một cú hích lớn về mặt tư duy. Sự kiện bước hẳn ra khỏi khuôn khổ kiến thức sách vở để mang đến những câu chuyện "xương máu" đúc rút từ môi trường doanh nghiệp thật. Một vài dấu ấn khó quên:

#### Học hỏi từ các diễn giả có chuyên môn cao

- Các diễn giả đến từ AWS Việt Nam, VPBank, VIB và Gothamic X đã cho tôi thấy khoảng cách thật sự giữa việc làm dự án cá nhân ở nhà và việc vận hành sản phẩm phục vụ hàng triệu khách hàng trong ngành Ngân hàng — nơi bảo mật thông tin và tính tuân thủ luôn là ưu tiên tối thượng.

#### Trải nghiệm kỹ thuật thực tế

- Thực sự "mở não" khi quan sát các AI Agent phối hợp theo mô hình Multi-Agent: tự động phân tích thị trường một cách toàn diện, từ chỉ số tài chính, dữ liệu mạng xã hội cho đến chân dung từng nhà sáng lập doanh nghiệp.
- Vỡ ra sự thật khốc liệt phía sau các thuật toán tối ưu chi phí của những nhà cung cấp Cloud lớn — và hiểu vì sao AI vẫn cho kết quả ngẫu nhiên ngay cả khi nhiệt độ đã đặt về không.

#### Ứng dụng công cụ hiện đại

- Chứng kiến dữ liệu được trực quan hóa chỉ bằng vài câu lệnh tiếng Việt giản đơn qua bản demo Amazon Q Business và QuickSight. Giao thức MCP (Model Context Protocol) thực sự mở ra một kỷ nguyên mới — nơi kỹ sư có thể chế tạo những "cánh tay nối dài" đúng nghĩa cho trí tuệ nhân tạo.

#### Kết nối và trao đổi

- Ban tổ chức đã kết nối rất khéo léo người tham dự giữa các tầng (kể cả các bạn ở tầng 36 thông qua hệ thống Lucky Draw). Sự kiện thắp lên tinh thần chủ động bắt chuyện, tìm kiếm cộng sự và truyền một nguồn cảm hứng làm việc nhóm mạnh mẽ cho các bạn sinh viên trẻ.

#### Bài học rút ra

- AI đang kéo chi phí phát triển phần mềm xuống thấp chưa từng thấy — nhu cầu thị trường vì thế sẽ bùng nổ, và cơ hội khổng lồ sẽ thuộc về những ai sở hữu tư duy hệ thống đủ tốt để giải các bài toán lớn.
- Tuyệt đối không lạm dụng AI theo lối sao chép nguyên văn (Ctrl+C & Ctrl+V) mà không hiểu bản chất mã nguồn — cái giá phải trả trên môi trường Production của doanh nghiệp là vô cùng đắt.
- Với một hệ thống công nghệ, "chạy được" chưa bao giờ là đích đến — nó phải chạy một cách **an toàn**, **đáng tin cậy** và thực sự **mang lại giá trị cho người dùng**.

#### Một số hình ảnh khi tham gia sự kiện

![Ảnh minh chứng: tham gia event](</images/4-EventParticipated/Event2/event2(0).jpg>)
![Ảnh minh chứng: tham gia event](</images/4-EventParticipated/Event2/evt2(1).jpg>)

> Nhìn lại toàn bộ sự kiện, giá trị nhận được không chỉ dừng ở khối kiến thức kỹ thuật chuyên sâu về Prompt Engineering hay mô hình phát triển phần mềm trong kỷ nguyên AI — điều đọng lại lớn hơn cả là ngọn lửa đam mê, tinh thần kỷ luật tự học và một tư duy nghề nghiệp đúng đắn được truyền lại cho thế hệ kỹ sư công nghệ kế tiếp.
