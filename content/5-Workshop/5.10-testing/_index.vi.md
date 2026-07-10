---
title: "Kiểm thử Ứng dụng"
date: 2024-01-01
weight: 10
chapter: false
pre: " <b> 5.10. </b> "
---
### 5.10. Kiểm thử Ứng dụng

Trong phần này, chúng ta sẽ thực hiện kiểm tra hoạt động thực tế của toàn bộ hệ thống Resume Fit thông qua các bước kiểm thử API và trải nghiệm chi tiết các chức năng giao diện người dùng.

---

#### 1. Kiểm thử Kết nối API và Cơ sở dữ liệu

Trước khi thao tác trên giao diện, ta cần đảm bảo các dịch vụ backend và cơ sở dữ liệu đã liên kết hoàn toàn thông qua Application Load Balancer.

1. Sử dụng trình duyệt hoặc công cụ dòng lệnh gửi request đến endpoint `/api/ready` của ALB:
   ```bash
   curl http://[ALB-DNS-Name]/api/ready
   ```
   Hệ thống sẽ phản hồi trạng thái sẵn sàng:
   ![ALB DNS Test](/img/Test_hoat_dong_bang_DNS_cua_ALB.jpg)
   
2. Kiểm tra log và trạng thái kết nối Database từ giao diện quản trị hoặc container log:
   ![Verify Connections](/img/Tien_hanh_kiem_tra_cac_ket_noi.jpg)

---

#### 2. Hướng dẫn chi tiết Giao diện người dùng Resume Fit

Dưới đây là quy trình chi tiết từng bước trải nghiệm các tính năng của nền tảng Resume Fit kèm theo hình ảnh minh họa thực tế:

##### 2.1. Đăng ký tài khoản (Register)
* **Mô tả:** Người dùng truy cập hệ thống lần đầu cần khởi tạo tài khoản. Giao diện tối giản cung cấp các trường nhập thông tin cơ bản: Họ tên, Email, và Mật khẩu.
* **Hình ảnh minh họa:**
  ![Giao diện Đăng ký](/img/giao%20di%E1%BB%87n/giao_dien_dang_ky.jpg)

##### 2.2. Đăng nhập hệ thống (Login)
* **Mô tả:** Sau khi tài khoản được kích hoạt, thực hiện đăng nhập để cấp quyền truy cập vào bảng điều khiển (Dashboard).
* **Hình ảnh minh họa:**
  ![Giao diện Đăng nhập](/img/giao%20di%E1%BB%87n/giao_dien_dang_nhap.jpg)

##### 2.3. Quản lý Yêu cầu Công việc (Job Descriptions List)
* **Mô tả:** Trang chủ hiển thị danh sách các vị trí tuyển dụng (JD) hiện tại đang hoạt động trên hệ thống. Tại đây, nhà tuyển dụng có thể theo dõi nhanh số lượng CV đã nộp và trạng thái lọc.
* **Hình ảnh minh họa:**
  ![Danh sách JD](/img/giao%20di%E1%BB%87n/giao_dien_danh_sach_JD.jpg)

##### 2.4. Bước 1: Tạo mô tả công việc (Create Job Description)
* **Mô tả:** Nhà tuyển dụng thực hiện thêm mới vị trí cần tuyển bằng cách điền tiêu đề công việc, yêu cầu kỹ năng bắt buộc và nội dung mô tả chi tiết của JD.
* **Hình ảnh minh họa:**
  ![Tạo JD mới](/img/giao%20di%E1%BB%87n/giao_dien_buoc_1_tao_ten_cong_viec_ung_tuyen.jpg)

##### 2.5. Bước 2: Tải lên hồ sơ ứng viên (Upload CVs)
* **Mô tả:** Chọn các file CV ứng viên dạng PDF để tải lên hệ thống tương ứng với vị trí công việc vừa chọn.
* **Hình ảnh minh họa:**
  ![Tải lên CV JD](/img/giao%20di%E1%BB%87n/giao_dien_buoc_2_upload_CV_JD.jpg)

##### 2.6. Theo dõi tiến trình tải lên (Upload Progress)
* **Mô tả:** Giao diện hiển thị thanh tiến trình xử lý real-time khi file được đẩy lên S3 và gửi thông điệp vào SQS để phân tích.
* **Hình ảnh minh họa:**
  ![Tiến trình tải lên](/img/giao%20di%E1%BB%87n/giao_dien_buoc_2_upload_CV_JD_Part-2.jpg)

##### 2.7. Danh sách hồ sơ ứng viên (CVs List)
* **Mô tả:** Hiển thị danh sách tất cả các ứng viên đã tải CV lên cho một vị trí công việc cụ thể.
* **Hình ảnh minh họa:**
  ![Danh sách CV](/img/giao%20di%E1%BB%87n/giao_dien_danh_sach_CV.jpg)

##### 2.8. Lịch sử đánh giá (Evaluation History)
* **Mô tả:** Nhật ký lưu trữ lịch sử các lần chạy đối khớp trước đó để nhà tuyển dụng dễ dàng so sánh hoặc tải lại kết quả cũ.
* **Hình ảnh minh họa:**
  ![Lịch sử đánh giá](/img/giao%20di%E1%BB%87n/giao_dien_lich_su_danh_gia_CV_JD.jpg)

##### 2.9. Xếp hạng ứng viên phù hợp (Candidate Matching Ranking)
* **Mô tả:** Thuật toán AI sắp xếp danh sách ứng viên theo thứ tự điểm số từ cao xuống thấp, giúp nhà tuyển dụng nhận diện nhanh các ứng cử viên sáng giá nhất.
* **Hình ảnh minh họa:**
  ![Xếp hạng ứng viên phù hợp](/img/giao%20di%E1%BB%87n/giao_dien_xep_hang_ung_vien_phu_hop.jpg)

##### 2.10. Bước 3: Xem chi tiết kết quả đánh giá (View Details)
* **Mô tả:** Click chọn một ứng viên cụ thể để truy cập báo cáo phân tích toàn diện được sinh ra từ mô hình AI.
* **Hình ảnh minh họa:**
  ![Xem kết quả ứng viên](/img/giao%20di%E1%BB%87n/giao_dien_buoc_3_xem_ket_qua_ung_vien.jpg)

##### 2.11. Đánh giá mức độ phù hợp (Overall Fit Score)
* **Mô tả:** Điểm số phần trăm (%) tổng quan thể hiện độ tương thích chung giữa hồ sơ ứng viên so với yêu cầu của JD.
* **Hình ảnh minh họa:**
  ![Đánh giá mức độ phù hợp](/img/giao%20di%E1%BB%87n/giao_dien_danh_gia_muc_do_phu_hop.jpg)

##### 2.12. Đánh giá kỹ năng (Skills Analysis)
* **Mô tả:** AI thực hiện đối sánh và liệt kê chi tiết các kỹ năng ứng viên đáp ứng (Matched Skills) và các kỹ năng còn thiếu sót (Missing Skills).
* **Hình ảnh minh họa:**
  ![Đánh giá kỹ năng](/img/giao%20di%E1%BB%87n/giao_dien_danh_gia_ky_nang.jpg)

##### 2.13. Đề xuất khuyến nghị (Hiring Recommendation)
* **Mô tả:** Đưa ra nhận xét định tính về điểm mạnh nổi bật, điểm cần cải thiện của ứng viên kèm theo kết luận đề xuất (Tuyển dụng / Cần phỏng vấn thêm / Từ chối).
* **Hình ảnh minh họa:**
  ![Đề xuất khuyến nghị](/img/giao%20di%E1%BB%87n/giao_dien_danh_gia_khuyen_nghi.jpg)

##### 2.14. Sinh câu hỏi phỏng vấn (Suggested Interview Questions)
* **Mô tả:** Dựa trên các kỹ năng bị thiếu hụt hoặc các điểm nghi vấn trong CV, AI tự động tạo ra bộ câu hỏi phỏng vấn chuyên sâu cho từng ứng viên.
* **Hình ảnh minh họa:**
  ![Sinh câu hỏi phỏng vấn](/img/giao%20di%E1%BB%87n/giao_dien_danh_gia_cau_hoi_phong_van.jpg)

##### 2.15. Phân tích chi tiết điểm số (Score Breakdown)
* **Mô tả:** Chi tiết hóa điểm số dựa trên nhiều khía cạnh khác nhau như: Học vấn, Kinh nghiệm làm việc, Kỹ năng cứng, Kỹ năng mềm.
* **Hình ảnh minh họa:**
  ![Phân tích điểm số](/img/giao%20di%E1%BB%87n/giao_dien_danh_gia_phan_tich_diem_so.jpg)

##### 2.16. Phân tích chi tiết hồ sơ ứng viên (Candidate Profile Analysis)
* **Mô tả:** Báo cáo tóm tắt quá trình làm việc, dự án nổi bật và lộ trình sự nghiệp được AI đúc kết từ CV.
* **Hình ảnh minh họa:**
  ![Chi tiết phân tích](/img/giao%20di%E1%BB%87n/giao_dien_danh_gia_phan_tich_ung_vien.jpg)

##### 2.17. Văn bản trích xuất (Extracted Raw Text)
* **Mô tả:** Xem lại toàn bộ phần văn bản thô đã trích xuất từ file CV gốc để kiểm tra tính toàn vẹn của dữ liệu đầu vào.
* **Hình ảnh minh họa:**
  ![Văn bản trích xuất](/img/giao%20di%E1%BB%87n/giao_dien_danh_gia_van_ban_trich_xuat.jpg)

##### 2.18. Bảng thông tin gỡ lỗi (Technical Debugger Panel)
* **Mô tả:** Cung cấp thông số kỹ thuật bao gồm thời gian xử lý API, dung lượng token tiêu thụ và logs hệ thống cho quản trị viên tối ưu hóa chi phí vận hành AI.
* **Hình ảnh minh họa:**
  ![Thông tin gỡ lỗi](/img/giao%20di%E1%BB%87n/giao_dien_thong_tin_go_loi_debugger.jpg)
