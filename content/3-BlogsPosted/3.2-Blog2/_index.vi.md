---
title: "Blog 2"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---
# Kinh Nghiệm Thực Chiến: Xây Dựng AI Gateway Quản Trị Amazon Bedrock Bằng API Gateway

Chào mọi người. Thời gian qua, trong lúc làm các lab hạ tầng AWS từ việc cấu hình mạng, gỡ lỗi bảo mật với Secrets Manager trong môi trường Cloud9, cho đến việc lên khung đề tài tích hợp Machine Learning vào Prometheus để giám sát hệ thống, mình vấp phải một bài toán khá khoai: Làm sao để quản lý quyền truy cập và kiểm soát chi phí khi các team bắt đầu xài chung các mô hình ngôn ngữ lớn (LLM) trên Amazon Bedrock?

Thực tế, khi build các ứng dụng Generative AI, mình không thể cứ thế quăng cái API key của Bedrock ra cho mọi người gọi trực tiếp được. Chi phí sẽ dội lên trời, và việc kiểm soát ranh giới dữ liệu giữa các người dùng (tenant isolation) gần như bằng không. Chật vật một thời gian, mình tìm thấy một kiến trúc tham chiếu (reference pattern) cực kỳ hay từ Dynatrace và quyết định áp dụng thử nghiệm. Hôm nay mình sẽ chia sẻ lại trải nghiệm thiết kế "AI Gateway" này dưới góc nhìn thực chiến.

### Kiến Trúc Tổng Quan - Gọn Nhẹ Nhưng Đầy Sức Mạng
Thay vì cho client "đâm thẳng" vào Bedrock, mình dựng một lớp khiên chắn bằng Amazon API Gateway làm trung tâm. Toàn bộ luồng đi sẽ được bóc tách như sau:

* **Route 53 (Tùy chọn nhưng nên có):** Thay vì xài cái endpoint dài ngoằng mặc định của AWS, mình dùng Route 53 để map một cái custom domain cho đẹp và chuẩn định dạng doanh nghiệp.
* **API Gateway (Cửa ngõ chính):** Nơi đây mình thiết lập các quy tắc về rate limiting (giới hạn tốc độ) để chống spam, và chia quota để không bị lố ngân sách. Điểm ăn tiền là nó hỗ trợ response streaming, nên khi ứng dụng cần stream text từ LLM về từng chữ một theo thời gian thực, mọi thứ diễn ra cực kỳ mượt mà.
* **Lambda Authorizer (Chốt chặn bảo mật):** Khách gọi API không thể tay không bắt giặc. Mình cấu hình một hàm Lambda để xác thực token JWT. Phải có thẻ hợp lệ thì mới được đi tiếp vào trong.
* **Lambda Integration (Trái tim của hệ thống):** Đây là phần mình ưng ý nhất. Hàm Lambda này đóng vai trò như một người chuyển phát nhanh mẫn cán. Nó chụp lấy toàn bộ request nguyên bản của người dùng (từ headers, body đến parameters), tự động ký xác thực bằng AWS Signature Version 4 (SigV4), rồi mới chuyển tiếp lệnh gọi đó đến đúng đích của Amazon Bedrock.

### Tại Sao Mình Lại Đánh Giá Cao Pattern Này?
Trong quá trình triển khai thực tế, mô hình này giải quyết được hai vấn đề cốt lõi mà dân làm hạ tầng cực kỳ quan tâm:

1. **Trải nghiệm code hoàn toàn trong suốt (Transparent to Client):** Mình thường xuyên test code ở local và xài thư viện Boto3 rất nhiều. Cái hay của gateway này là khi gọi API, code phía client gần như không phải sửa chữa gì. Hệ thống bên ngoài cứ tưởng là đang giao tiếp trực tiếp với Bedrock, nhưng thực ra mọi thứ đã đi qua một lớp kiểm duyệt gắt gao ngầm phía sau.
2. **Khả năng bắt trend không giới hạn (Future-proof Design):** Mọi người làm Cloud đều biết AWS cập nhật tính năng mới cho Bedrock liên tục. Nếu gateway mà phải hardcode từng API endpoint thì mỗi lần có model mới ra mắt là một lần sửa code sấp mặt. Nhờ thiết kế của hàm Lambda Integration chỉ làm nhiệm vụ "đóng gói và ký gửi" chứ không can thiệp sâu vào cấu trúc API nên ngày mai Bedrock có ra mắt thêm model nào mới hay cập nhật tính năng Knowledge Bases, hệ thống của mình vẫn chạy ổn định mà không cần đụng đến một dòng code bảo trì nào.

### Kết Lại
Vốn là làm về các hệ thống giám sát và trực quan hóa dữ liệu (như Grafana hay Zabbix), việc quy tụ mọi luồng traffic AI về một cổng API Gateway duy nhất giúp mình cực kỳ dễ dàng cắm các tool monitoring vào để theo dõi sức khỏe hệ thống và chi phí từng project.

Việc tận dụng các dịch vụ Serverless để làm lớp quản trị cho AI không chỉ gia tăng tính bảo mật mà còn tối ưu hóa đáng kể khâu vận hành. Nếu mọi người cũng đang xây dựng hạ tầng cho các ứng dụng GenAI trên AWS, mô hình AI Gateway này chắc chắn là một mảnh ghép đáng để đưa vào hệ thống.

![Sơ đồ kiến trúc](/images/blog2_arch.png)

* [Link bài viết Facebook](https://www.facebook.com/groups/awsstudygroupfcj/permalink/2179637596134534/?rdid=654DT9MyMTrqQ5kg#)
* [Tài liệu hướng dẫn AWS](https://aws.amazon.com/vi/blogs/architecture/building-an-ai-gateway-to-amazon-bedrock-with-amazon-api-gateway/)