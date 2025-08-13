---
title : "Giới thiệu"
weight : 1 
chapter : false
pre : " <b> 1. </b> "
---

**Triển khai hệ thống quản lý artifact an toàn với AWS CodeArtifact và quét bảo mật tự động** là một workshop thực hành giúp bạn xây dựng quy trình DevSecOps hoàn chỉnh — từ khâu **build**, **scan bảo mật**, **quản lý truy cập**, đến **giám sát compliance**.

Workshop tập trung vào:
- Quản lý artifact (npm, Maven, Docker...) tập trung, an toàn.
- Tự động quét lỗ hổng bảo mật trước khi artifact được phát hành.
- Ghi log, cảnh báo và lưu trữ bằng AWS CloudWatch & CloudTrail.
- Mã hóa artifact và log bằng AWS KMS.
- Thiết lập quyền truy cập chi tiết theo nguyên tắc **least privilege** với IAM.

---

## **2. Kiến trúc tổng quan**

Giải pháp được xây dựng theo kiến trúc cloud-native, tích hợp nhiều dịch vụ AWS:

- **AWS CodeArtifact**: Lưu trữ artifact với versioning và kiểm soát truy cập.
- **Amazon ECR (Enhanced Scanning)**: Quét bảo mật container image.
- **Snyk**: Quét dependency và phát hiện CVE cho npm, Maven, Python...
- **Amazon CodeGuru Reviewer**: Phân tích code tự động, phát hiện lỗ hổng và best practice violations.
- **AWS IAM & AWS KMS**: Quản lý quyền truy cập, mã hóa dữ liệu.
- **CloudWatch Logs & Metrics, CloudTrail**: Giám sát và lưu lại mọi hoạt động.
- **SNS / EventBridge**: Gửi cảnh báo tự động khi phát hiện sự cố.

![VPC](/images/zzz/AD.png)

**Luồng hoạt động chính:**
1. Developer push code lên GitHub → GitHub Actions khởi động pipeline.
2. Pipeline build → chạy quét bảo mật (Snyk, CodeGuru, ECR).
3. Artifact pass kiểm tra → upload lên CodeArtifact / ECR; fail → gửi cảnh báo và ghi log.
4. CloudWatch & CloudTrail ghi lại toàn bộ quá trình, Audit Manager thu thập evidence phục vụ compliance.
