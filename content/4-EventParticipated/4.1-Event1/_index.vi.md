---
title: "Event 1"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---
# Bài thu hoạch: FCAJ Community Day

### Mục Đích Của Sự Kiện
*   **Mục tiêu của chương trình:** Tạo môi trường và cơ hội để các bạn trẻ (đặc biệt là sinh viên năm 3, năm 4 hoặc mới ra trường) mạnh dạn chia sẻ kiến thức, rèn luyện kỹ năng thuyết trình, thái độ tự tin trước đám đông và định hướng phát triển sự nghiệp.
*   **Nội dung chính muốn truyền tải:** Cách tạo động lực học tập (hack dopamine), kỹ thuật tối ưu hóa câu lệnh AI (Prompt Engineering), định hướng tư duy cốt lõi trong ngành IT giữa kỷ nguyên AI, và quy trình chuẩn ứng dụng AI vào phát triển phần mềm (phương pháp BMX).
*   **Giá trị dành cho người tham dự:** Giúp người tham dự vượt qua nỗi sợ bị AI thay thế, hiểu được tầm quan trọng của kiến thức nền tảng (foundation), biết cách vận dụng công cụ đúng quy trình và định hình các yếu tố cốt lõi khi phát triển sự nghiệp như "sự liêm chính" (integrity) và tư duy dài hạn.

### Danh Sách Diễn Giả
*   **Long** – Chủ đề trình bày: Hack não bộ với Dopamine.
*   **Thịnh** – Chủ đề trình bày: Ultimate Prompt Engineering và kiến trúc AWS.
*   **Khang** – Chức vụ: Solutions Architect (Cloud Kinetics).
*   **Thảo** – Chức vụ: Software Developer (Ngân hàng Quốc tế Việt Nam - VIB).

### Nội Dung Nổi Bật
*   **Tổng quan vấn đề:** Sinh viên và người đi làm thường thiếu động lực học tập, dễ bị phân tâm bởi mạng xã hội do thiếu "phần thưởng nhanh". Ngoài ra, trong môi trường làm việc, việc quá phụ thuộc vào AI để viết code trực tiếp mà thiếu bối cảnh sẽ tạo ra những đoạn code rác, thiếu đồng bộ (ảo giác/hallucination của AI).
*   **Giải pháp được giới thiệu:** 
    *   Để học tập hiệu quả, cần chia nhỏ mục tiêu, tạo phần thưởng ngắn hạn, xây dựng "chuỗi" liên tục (như chơi game) để đánh lừa não bộ tiết ra dopamine. 
    *   Để làm chủ AI, phải tập trung vào "nền tảng" (foundation), chia nhỏ task ra thành các văn bản mô tả (document) theo phương pháp BMX trước khi để AI sinh code.
*   **Công nghệ/Dịch vụ/Công cụ:** 
    *   **AWS:** CloudFront, S3 (lưu trữ), Cognito (xác thực), API Gateway, Lambda (serverless backend), Bedrock (AI models), DynamoDB (NoSQL Database), CloudWatch (Monitoring).
    *   **Công cụ AI:** Các mô hình LLMs (Claude, Gemini), extension "Promptimizer", framework BMX.
*   **Demo hoặc Case Study:** 
    *   Trình bày một kiến trúc thực tế xây dựng trên AWS kết hợp nhiều dịch vụ Serverless và AI.
    *   Demo sử dụng tiện ích mở rộng có tên "Promptimizer" để bôi đen văn bản và nhờ AI tối ưu hóa Prompt ngay trên trình duyệt.
*   **Các điểm đáng chú ý:** Việc dùng AI sẽ **khuếch đại (amplify)** khả năng của người dùng: nếu bạn hiểu biết kém, nó sẽ làm kết quả tệ hơn, nếu bạn có nền tảng vững, nó sẽ giúp bạn tăng năng suất gấp nhiều lần. 

### Những Gì Học Được
*   **Tư duy và phương pháp:** Có thể dùng AI để hỗ trợ quá trình suy nghĩ (brainstorm), nhưng tuyệt đối **không được "outsource" sự hiểu biết của chính mình**. Luôn luôn phải đặt câu hỏi **"Tại sao" (Why)** cho mọi quyết định kỹ thuật.
*   **Kiến thức kỹ thuật:** Cấu trúc thành phần trong Prompt Engineering hiệu quả bao gồm: Role (vai trò), Instruction (hướng dẫn), Context (ngữ cảnh), Input, Output Format (định dạng) và Constraints (ràng buộc).
*   **Best practices:** Để AI không bị lỗi bối cảnh, cần chia nhỏ yêu cầu đầu vào thay vì nhồi nhét. Trong quy trình phát triển, hãy để AI đóng vai trò của từng bộ phận riêng biệt (BM, Architect, Dev, Scrum Master) xử lý từng tính năng nhỏ (story) được duyệt kỹ lưỡng thay vì phó mặc toàn bộ dự án.
*   **Kinh nghiệm thực tế:** Khi tuyển dụng, nhà tuyển dụng không chỉ cần kết quả đúng mà chú trọng **quá trình tư duy (thought process)** và lý do ứng viên chọn giải pháp đó. Kinh nghiệm không đếm bằng thời gian làm việc mà đếm bằng số lượng "trải nghiệm" xử lý các bài toán, dự án khác nhau.

### Ứng Dụng Vào Công Việc
*   **Có thể áp dụng gì cho dự án hiện tại:** Thay đổi cách lập trình phần mềm với AI bằng việc đầu tư viết kỹ Document (VOD, System Architect) trước. Phân rã dự án thành Epic, Story rồi mới để AI agent code và tự động review lỗi cho từng phần đó. 
*   **Công nghệ muốn thử nghiệm:** Ứng dụng AWS Lambda, Amazon Cognito để làm backend serverless mà không cần tự quản lý server hay database mật khẩu người dùng. Cài đặt và sử dụng extension "Promptimizer" để tăng chất lượng giao tiếp với các mô hình ngôn ngữ.
*   **Ý tưởng cải thiện quy trình làm việc:** Áp dụng **quy tắc 2 phút**: việc gì giải quyết được trong vòng 2 phút thì phải làm ngay, không trì hoãn.

### Trải nghiệm trong event
*   **Học hỏi từ diễn giả:** Nhận thức rõ về 5 yếu tố quyết định khi đi làm: Salary (Lương), Experience (Kinh nghiệm), Network (Mạng lưới), Knowledge (Kiến thức) và Profile (Hồ sơ). 
*   **Trải nghiệm thực hành:** Việc xem các case study thiết kế kiến trúc hệ thống và demo thao tác trực tiếp với Promptimizer mang lại hình dung rất thực tế và sinh động.
*   **Giao lưu và kết nối:** Cộng đồng động viên các thành viên (kể cả sinh viên) không sợ sai, không sợ chia sẻ điều người khác đã biết, đề cao tính làm việc nhóm (teamwork) để đi xa thay vì đi một mình.
*   **Điều ấn tượng nhất:** Quan điểm về **"Sự liêm chính" (Integrity)** - đó là việc tự giác xử lý toàn bộ các tình huống ngoại lệ (corner cases) và làm tốt mọi nhiệm vụ dù sếp có kiểm tra hay không, và tính chịu trách nhiệm với sự tin tưởng trong đường dài.

### Bài Học Rút Ra
*   **Kiến thức quan trọng nhất:** Nắm thật chắc **kiến thức nền tảng (foundation)**; chỉ khi hiểu tận gốc vấn đề bạn mới có khả năng thẩm định xem kết quả do AI sinh ra đúng hay sai.
*   **Kinh nghiệm thực tế:** Sai lầm là điều cần thiết để phát triển, đặc biệt ở giai đoạn "fresher". Các công ty sẵn sàng trả chi phí cho sai lầm của bạn miễn là bạn có tư duy học hỏi và sửa đổi.
*   **Định hướng học tập hoặc phát triển tiếp theo:** Tập thói quen theo dõi những cập nhật mới từ AWS hay công nghệ để tổng hợp kiến thức, định hướng trở thành người có thể trình bày/chia sẻ kiến thức (speaker) thay vì tiêu thụ nội dung vô bổ. Phát triển môi trường học tập bền bỉ và kiên trì, không mong đợi kết quả trong chớp mắt.

### Một số hình ảnh khi tham gia sự kiện
![Ảnh sự kiện 1](/images/event1_1.png)
![Ảnh sự kiện 2](/images/event1_2.png)
![Ảnh sự kiện 3](/images/event1_3.png)
![Ảnh sự kiện 4](/images/event1_4.png)

> Tổng thể, sự kiện không chỉ cung cấp kiến thức kỹ thuật mà còn giúp tôi thay đổi cách tư duy về thiết kế ứng dụng, hiện đại hóa hệ thống và phối hợp hiệu quả hơn giữa các team.
