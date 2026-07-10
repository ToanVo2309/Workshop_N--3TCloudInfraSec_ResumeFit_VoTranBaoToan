---
title: "Blog 1"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---
# GIÁM SÁT HỆ THỐNG TRÊN AWS: ĐƯA CLOUDWATCH METRICS VÀO OPENTELEMETRY COLLECTOR TRONG VPC BẰNG LAMBDA

Quản lý giám sát (observability) cho các hệ thống đám mây quy mô lớn luôn là một bài toán đầy thách thức, đặc biệt khi doanh nghiệp muốn cân bằng giữa chi phí, tính linh hoạt và bảo mật. Dù OpenTelemetry đang dần trở thành tiêu chuẩn chung giúp các tổ chức thoát khỏi sự phụ thuộc vào bên thứ ba (vendor lock-in), họ lại vấp phải một rào cản kỹ thuật lớn: làm thế nào để luân chuyển các chỉ số (metrics) từ AWS CloudWatch vào thẳng các hệ thống thu thập nội bộ được cô lập nghiêm ngặt trong VPC? Để gỡ rối vấn đề này, giải pháp sử dụng AWS Lambda đóng vai trò như một trạm trung chuyển dữ liệu từ CloudWatch Metric Streams đến mạng nội bộ đã chứng minh tính hiệu quả vượt trội, đảm bảo luồng dữ liệu luôn được truyền tải an toàn và tức thời.

### DƯỚI ĐÂY LÀ NHỮNG ĐIỂM NỔI BẬT VỀ GIẢI PHÁP PUSH-BASED OBSERVABILITY NÀY:
* **Chuyển dịch từ Pull sang Push model:** Việc dùng các công cụ như Prometheus liên tục "kéo" (pull/poll) dữ liệu gây ra tình trạng quá tải API (throttling), thất thoát metrics và tốn kém chi phí. Mô hình "đẩy" (Push) với CloudWatch Metric Streams giải quyết triệt để vấn đề này, giúp truyền dữ liệu dựa trên sự kiện với độ trễ dưới một phút (sub-minute latency) phục vụ cho cảnh báo thời gian thực.
* **Vượt qua giới hạn của Amazon Data Firehose:** Dù Firehose hỗ trợ đẩy dữ liệu ra các HTTP endpoint, nhưng nó lại bắt buộc đó phải là các endpoint công khai (public). Để đưa dữ liệu vào private subnet, AWS sử dụng một hàm Lambda (Lambda Transform Function) làm cầu nối. Firehose sẽ gom dữ liệu và gọi Lambda; sau đó Lambda sẽ đẩy metrics qua NLB vào sâu trong VPC một cách bảo mật.
* **OpenTelemetry Collector là trái tim của hệ thống:** Chạy trên các Amazon EC2 instance bên trong VPC, Collector hoạt động như một trung tâm xử lý với 3 thành phần linh hoạt: Receivers (tiếp nhận dữ liệu), Processors (lọc, làm giàu (Enriched Data), che giấu dữ liệu nhạy cảm) và Exporters (xuất dữ liệu đến các đích đến đa dạng như Grafana, AWS X-Ray, hay Amazon OpenSearch).
* **Khả năng mở rộng và dự phòng an toàn:** Nhờ sử dụng Network Load Balancer phân phối tải TCP đến các EC2 instance, hệ thống có thể dễ dàng mở rộng theo chiều ngang. Ngoài ra, một Amazon S3 bucket được cấu hình làm điểm đến dự phòng cho Firehose (tuy nhiên sẽ không phát sinh chi phí lưu trữ nếu Lambda đã đẩy dữ liệu thành công).
* **Tối ưu chi phí và loại bỏ Vendor Lock-in:** Sử dụng OpenTelemetry (giấy phép Apache 2.0 hoàn toàn miễn phí) giúp doanh nghiệp gạt bỏ gánh nặng chi phí bản quyền phần mềm bên thứ ba. Tính chuẩn hóa của nó cho phép team vận hành tự do thay đổi các nền tảng giám sát backend sau này mà không cần đập đi xây lại luồng thu thập dữ liệu.

Nhìn chung, việc kết hợp khéo léo các dịch vụ AWS như Lambda, Firehose và Network Load Balancer đã tạo ra một cầu nối hoàn hảo, xóa bỏ khoảng cách giữa dịch vụ đám mây công cộng và mạng nội bộ khép kín. Kiến trúc này không chỉ xử lý triệt để bài toán về độ trễ hay giới hạn của các API truyền thống, mà còn trao quyền tối đa cho các đội ngũ kỹ thuật. Bằng cách thiết lập một luồng truyền dữ liệu thông minh, doanh nghiệp hoàn toàn có thể tự do xây dựng một hệ sinh thái giám sát mạnh mẽ, độc lập, tối ưu ngân sách và luôn sẵn sàng mở rộng trong tương lai mà không lo ngại về rủi ro phụ thuộc công nghệ.

Xây dựng hệ thống giám sát không khó, cái khó là làm sao để nó bảo mật, ít tốn kém và không bị phụ thuộc công nghệ. Bạn đánh giá thế nào về kiến trúc Push-based với Lambda và OpenTelemetry này? Nếu đang trực tiếp vận hành hệ thống, rào cản lớn nhất của bạn hiện tại là câu chuyện bảo mật (đưa metrics vào private VPC an toàn) hay bài toán tối ưu chi phí hạ tầng? Cùng thảo luận nhé!

![Sơ đồ kiến trúc](/images/blog1_arch.png)

* [Link bài viết Facebook](https://www.facebook.com/groups/awsstudygroupfcj/permalink/2173544653410495/?rdid=CUzsR7GSYpgaIwjW)
* [Tài liệu hướng dẫn AWS](https://aws.amazon.com/vi/blogs/architecture/streaming-cloudwatch-metrics-to-vpc-based-opentelemetry-collectors-using-lambda/)