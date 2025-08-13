---
title : "Tích hợp CI/CD + Scanning"
weight : 3
chapter : false
date : 2025-08-12
pre : " <b> 3. </b> "
---

{{% notice info %}}
Chúng ta tích hợp pipeline CI/CD sử dụng **GitHub Actions** để tự động build, quét bảo mật và publish artifact lên AWS CodeArtifact/ECR.  
Các công cụ bảo mật như **Snyk** và **ECR Enhanced Scanning** sẽ được áp dụng để phát hiện lỗ hổng trước khi artifact được phát hành.
{{% /notice %}}

Trong phần này, chúng ta sẽ:
- Tạo workflow GitHub Actions kết nối với AWS.
- Cấu hình bước build, quét bảo mật với Snyk.
- Tích hợp quét container image bằng ECR Enhanced Scanning.
- Tự động publish artifact khi pass kiểm tra.

---

### **Nội dung thực hành**
- [Tạo GitHub Actions Workflow cơ bản](3.1-create-github-actions-workflow/)
- [Tích hợp quét container với ECR Enhanced Scanning](3.2-integrate-ecr-scanning/)
- [Kiểm tra và xác nhận pipeline hoạt động](3.3-verify-pipeline/)
