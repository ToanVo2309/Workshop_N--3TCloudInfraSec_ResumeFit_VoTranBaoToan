---
title: "Event 2"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 4.2. </b> "
---
# Bài thu hoạch: FCAJ Community Day

### Mục Đích Của Sự Kiện
*   **Mục tiêu của chương trình:** Không chỉ để nghe hội thảo, mà là nơi để kết nối, giao lưu, và truyền cảm hứng cho nhau (biết đâu sẽ gặp đối tác hoặc người bạn mới).
*   **Nội dung chính muốn truyền tải:** Xoay quanh các chủ đề từ AI, Cloud, đến những câu chuyện thực tế được đúc kết từ kinh nghiệm của các chuyên gia trong ngành. Bàn về việc tối ưu hóa cách dùng Prompt, các công nghệ của AWS (như CloudFront), hành trình thi Hackathon, và tư duy xây dựng kiến trúc AI nghiệp vụ (Enterprise grade).
*   **Giá trị dành cho người tham dự:** Giúp người tham dự hiểu rõ thị trường việc làm biến động ra sao dưới tác động của AI, cách chuẩn bị nền tảng để không bị đào thải, và trang bị tư duy giải quyết vấn đề thực tế cho doanh nghiệp.

### Danh Sách Diễn Giả
*   **Quỳnh Mai** – Vai trò: MC.
*   **Nguyễn Gia Hưng** – Chức vụ: Head of Solution Architect (AWS Vietnam), Founder của FCAJ.
*   **Tịnh** – Chức vụ: Platform Engineer (Gotam X).
*   **Hải Anh** – Đơn vị công tác: Pacific Vietnam (từng trình bày tại AWS Singapore Summit và Silicon Valley).
*   **Thịnh** – Chức vụ: DevOps Engineer (UTM Group, nhóm Developers) – Trình bày về dự án Hackathon của nhóm.
*   **Đức** – Chuyên môn: Chuyên gia tối ưu hóa Large Language Models (LLM Optimization).
*   **Vy** – Đơn vị công tác: VPBank (Vietnam Prosperity Joint Stock Commercial Bank) – Trình bày về hệ thống Enterprise Multi-Agent.

### Nội Dung Nổi Bật
*   **Tổng quan vấn đề:** AI khiến chi phí tạo phần mềm rẻ đi, do đó nhu cầu phần mềm sẽ tăng khủng khiếp, tạo ra rất nhiều việc làm mới trong mảng vận hành (Platform engineering) và sửa lỗi (fix code của AI). Một vấn đề khác là việc sinh code bằng AI nhưng thiếu ngữ cảnh sẽ tạo ra rác (ảo giác LLM).
*   **Giải pháp được giới thiệu:** 
    *   Cần thiết lập ngữ cảnh (Context/System Prompt) rõ ràng khi dùng AI, bao gồm: Goal, Persona, Format thay vì chỉ hỏi lan man.
    *   Sử dụng cơ chế Multi-Agent System (Hệ thống đa tác tử) để giải quyết các bài toán phức tạp (như phân tích tín dụng cho Startup) thay vì nhồi nhét mọi thứ vào một con AI.
*   **Công nghệ/Dịch vụ/Công cụ:** 
    *   **AWS:** CloudFront (Flat-rate pricing, content compression, chống DDoS), AWS Bedrock, EC2, Lambda, VPC.
    *   **AI/LLM:** Amazon Agent platform, Obsidian (để build Second Brain), MCP (Model Context Protocol).
    *   **Khác:** Terraform (Infrastructure as Code).
*   **Demo hoặc Case Study:** 
    *   *Dự án UTM Morpo:* Demo công cụ dùng 3 AI agents tạo HTML/UI từ hình ảnh và cho phép người dùng kéo thả, edit trực tiếp trên giao diện trong giải Hackathon.
    *   *Demo Tham số LLM:* Chạy so sánh Temperature = 0 trên AWS Bedrock và trên Local để chứng minh rằng ở trên Cloud, câu trả lời của AI vẫn có sự chênh lệch do cơ chế tối ưu hóa (Inference Optimization).
*   **Các điểm đáng chú ý:** Trong môi trường Enterprise (doanh nghiệp), việc tuân thủ bảo mật và đánh giá rủi ro (Guardrails, Security, Audit) là tối quan trọng, quan trọng hơn việc cắm được bao nhiêu công cụ cho AI.

### Những Gì Học Được
*   **Tư duy và phương pháp:** LLM là một "Probabilistic engine" (mô hình xác suất), do đó đừng mặc định nó luôn trả về cùng một kết quả dù có setup Temperature = 0. Đừng để AI "auto-pilot" hoàn toàn mà luôn phải có con người kiểm duyệt (Human in the loop).
*   **Kiến thức kỹ thuật:** Hiểu cách CloudFront tối ưu chi phí thông qua cơ chế gói Flat-rate (trả phí cố định) để tránh bị "bill sốc" do lượng truy cập hoặc bị tấn công DDoS.
*   **Best practices:** Tránh hội chứng "Internet puller" (thấy tool hay code gì trên mạng cũng bê nguyên vào dự án mà không hiểu ngữ cảnh).
*   **Kinh nghiệm thực tế:** Khi đi thi Hackathon, việc có quá nhiều ý tưởng (over-generation) sẽ làm mất thời gian. Cần giới hạn scope, tập trung vào giải quyết một vấn đề cốt lõi nhất (như tăng cường trải nghiệm edit) để kịp hoàn thành trong 36 tiếng.

### Ứng Dụng Vào Công Việc
*   **Có thể áp dụng gì cho dự án hiện tại:** Thiết kế hệ thống AI theo chuẩn Multi-agent: giao việc cụ thể cho từng agent chuyên biệt (VD: Agent phân tích tài chính, Agent nghiên cứu thị trường). Xây dựng mTLS và VPC Origin để bảo mật tài nguyên.
*   **Công nghệ muốn thử nghiệm:** Áp dụng Terraform để deploy hạ tầng bằng code (IaC) giúp quản lý phiên bản dễ dàng. Thử nghiệm các tính năng bảo vệ biên của AWS CloudFront (chặn truy cập theo khu vực, block bot).
*   **Ý tưởng cải thiện quy trình làm việc:** Thay vì tải dữ liệu thủ công, có thể dùng AI Agent tích hợp với thư viện (như MCP kết nối Excel) để nó tự động tạo dashboard phân tích hoặc tóm tắt nội dung meeting.

### Trải nghiệm trong event
*   **Học hỏi từ diễn giả:** Nhận ra rằng khi đi làm, nhà tuyển dụng không chỉ hỏi demo mà sẽ hỏi về "Sản phẩm" (Product) thực tế và các Use case nghiệp vụ.
*   **Trải nghiệm thực hành:** Xem trực tiếp demo xây dựng app 36 giờ, và xem minh họa trực quan sự khác biệt của LLM khi chạy local so với cloud.
*   **Giao lưu và kết nối:** Khuyến khích sự tự tin, dám đứng lên trình bày (từ một bạn sinh viên đến các diễn giả) vì tỷ lệ chọi khi xin việc thực tế là cực kỳ khốc liệt.
*   **Điều ấn tượng nhất:** Quan điểm cảnh tỉnh mạnh mẽ về việc copy nguyên code từ ChatGPT dán vào hệ thống doanh nghiệp sẽ gây họa (hỏng coding standard, lủng bảo mật).

### Bài Học Rút Ra
*   **Kiến thức quan trọng nhất:** Kiến thức nền tảng (Foundation), bằng đại học, và các kỹ năng phát triển phần mềm cơ bản (Software Engineering) vẫn là bắt buộc. AI chỉ là điểm cộng, không thể thay thế kỹ thuật phần mềm cốt lõi (như biết cách decode/encode password an toàn).
*   **Kinh nghiệm thực tế:** Để thuyết phục các sếp lớn cấp kinh phí làm AI (chẳng hạn 1 tỷ đồng), phải chỉ ra được ROI (Tỉ suất hoàn vốn) và các con số tiết kiệm thực tế, "Numbers speak louder than words".
*   **Định hướng học tập hoặc phát triển tiếp theo:** Đi sâu vào tìm hiểu AI Mindset và AI Adoption. Luôn nhớ quy tắc khi xây dựng hệ thống: Không chỉ chạy được, mà nó "phải chạy một cách an toàn, chạy đáng tin cậy và phục vụ người dùng". Đọc kỹ tài liệu chính thức (official doc) khi cấu hình tham số AI thay vì nghe trên mạng.

### Một số hình ảnh khi tham gia sự kiện
![Ảnh sự kiện 1](/images/event2_1.jpg)
![Ảnh sự kiện 2](/images/event2_2.jpg)
![Ảnh sự kiện 3](/images/event2_3.jpg)
![Ảnh sự kiện 4](/images/event2_4.jpg)

> Tổng thể, sự kiện không chỉ cung cấp kiến thức kỹ thuật mà còn giúp tôi thay đổi cách tư duy về thiết kế ứng dụng, hiện đại hóa hệ thống và phối hợp hiệu quả hơn giữa các team.
