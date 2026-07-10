---
title: "Verification and Testing"
date: 2024-01-01
weight: 10
chapter: false
pre: " <b> 5.10. </b> "
---
### 5.10. Verification and Testing

In this section, we will verify the end-to-end functionality of the deployed Resume Fit platform through API endpoint verification and a step-by-step user interface walkthrough.

---

#### 1. API and Database Connection Test

Before exploring the web UI, ensure that backend services and database connectivity are fully verified via the Application Load Balancer.

1. Query the ALB health endpoint using a web browser or curl:
   ```bash
   curl http://[ALB-DNS-Name]/api/ready
   ```
   The backend should return a healthy status:
   ![ALB DNS Test](/img/Test_hoat_dong_bang_DNS_cua_ALB.jpg)
   
2. Check database connection status and server logs from the management console:
   ![Verify Connections](/img/Tien_hanh_kiem_tra_cac_ket_noi.jpg)

---

#### 2. Detailed Resume Fit User Interface Guide

Below is a detailed walkthrough of the Resume Fit user interface features, accompanied by actual application screenshots:

##### 2.1. User Registration (Register)
* **Description:** First-time users can register an account. The clean interface provides standard fields: Full Name, Email, and Password.
* **Screenshot:**
  ![Register UI](/img/giao%20di%E1%BB%87n/giao_dien_dang_ky.jpg)

##### 2.2. System Login (Login)
* **Description:** Access the main recruiter Dashboard by authenticating with the newly created credentials.
* **Screenshot:**
  ![Login UI](/img/giao%20di%E1%BB%87n/giao_dien_dang_nhap.jpg)

##### 2.3. Job Descriptions Management (JD List)
* **Description:** The homepage displays currently active job openings (JDs). Recruiters can track the number of applicant CVs and review the screening status.
* **Screenshot:**
  ![JD list UI](/img/giao%20di%E1%BB%87n/giao_dien_danh_sach_JD.jpg)

##### 2.4. Step 1: Create Job Description
* **Description:** Recruiters can publish a new job opening by entering the job title, mandatory core skills, and a detailed description.
* **Screenshot:**
  ![Create JD UI](/img/giao%20di%E1%BB%87n/giao_dien_buoc_1_tao_ten_cong_viec_ung_tuyen.jpg)

##### 2.5. Step 2: Upload Resumes (CVs)
* **Description:** Select and upload candidate CV files (PDF format) corresponding to the chosen job description.
* **Screenshot:**
  ![Upload CV JD](/img/giao%20di%E1%BB%87n/giao_dien_buoc_2_upload_CV_JD.jpg)

##### 2.6. Monitor Upload Progress
* **Description:** The interface provides a real-time progress bar as files are uploaded to S3 and queued into SQS for asynchronous AI processing.
* **Screenshot:**
  ![Uploading progress](/img/giao%20di%E1%BB%87n/giao_dien_buoc_2_upload_CV_JD_Part-2.jpg)

##### 2.7. Applicant Resumes List (CVs List)
* **Description:** View all candidate profiles associated with a specific job description.
* **Screenshot:**
  ![CV list UI](/img/giao%20di%E1%BB%87n/giao_dien_danh_sach_CV.jpg)

##### 2.8. Evaluation History
* **Description:** Access historical matching logs, allowing recruiters to review past results easily.
* **Screenshot:**
  ![Evaluation history UI](/img/giao%20di%E1%BB%87n/giao_dien_lich_su_danh_gia_CV_JD.jpg)

##### 2.9. Candidate Matching Ranking
* **Description:** The AI algorithm automatically ranks candidates based on their compatibility scores from high to low.
* **Screenshot:**
  ![Candidate ranking UI](/img/giao%20di%E1%BB%87n/giao_dien_xep_hang_ung_vien_phu_hop.jpg)

##### 2.10. Step 3: View Analysis Report
* **Description:** Select a candidate to view the comprehensive AI evaluation report.
* **Screenshot:**
  ![Candidate results UI](/img/giao%20di%E1%BB%87n/giao_dien_buoc_3_xem_ket_qua_ung_vien.jpg)

##### 2.11. Overall Fit Score
* **Description:** An overall percentage compatibility score matching candidate credentials against the job requirements.
* **Screenshot:**
  ![Fit score rating UI](/img/giao%20di%E1%BB%87n/giao_dien_danh_gia_muc_do_phu_hop.jpg)

##### 2.12. Skills Gap Analysis (Skills)
* **Description:** Detailed analysis mapping the candidate's matched skills alongside missing skills.
* **Screenshot:**
  ![Skills matching UI](/img/giao%20di%E1%BB%87n/giao_dien_danh_gia_ky_nang.jpg)

##### 2.13. Hiring Recommendation
* **Description:** Qualitative evaluation detailing the candidate's strengths and areas for improvement, accompanied by a final hiring decision suggestion.
* **Screenshot:**
  ![Hiring recommendations UI](/img/giao%20di%E1%BB%87n/giao_dien_danh_gia_khuyen_nghi.jpg)

##### 2.14. Suggested Interview Questions
* **Description:** AI-generated tailored interview questions targeting the candidate's identified skills gaps.
* **Screenshot:**
  ![Generated questions UI](/img/giao%20di%E1%BB%87n/giao_dien_danh_gia_cau_hoi_phong_van.jpg)

##### 2.15. Score Breakdown
* **Description:** Granular compatibility breakdown across education, experience, hard skills, and soft skills.
* **Screenshot:**
  ![Score breakdown UI](/img/giao%20di%E1%BB%87n/giao_dien_danh_gia_phan_tich_diem_so.jpg)

##### 2.16. Candidate Profile Analysis
* **Description:** Summarized report highlighting candidate work experience, key projects, and career path analysis.
* **Screenshot:**
  ![Detailed analysis UI](/img/giao%20di%E1%BB%87n/giao_dien_danh_gia_phan_tich_ung_vien.jpg)

##### 2.17. Extracted Raw Text
* **Description:** Review the raw text extracted from the CV file to verify input data completeness.
* **Screenshot:**
  ![Extracted text UI](/img/giao%20di%E1%BB%87n/giao_dien_danh_gia_van_ban_trich_xuat.jpg)

##### 2.18. Technical Debugger Panel
* **Description:** Displays processing logs, API response times, and token usage metrics to optimize cost and performance.
* **Screenshot:**
  ![Debug panel UI](/img/giao%20di%E1%BB%87n/giao_dien_thong_tin_go_loi_debugger.jpg)
