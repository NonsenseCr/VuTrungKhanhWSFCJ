---
title : "Các bước chuẩn bị"
weight : 2 
chapter : false
date : 2025-08-12
pre : " <b> 2. </b> "
---

{{% notice info %}}
Chuẩn bị sẵn **AWS Account** có quyền tạo tài nguyên (IAM, CodeArtifact, KMS, ECR, CloudWatch...) và một **GitHub Repository** để triển khai pipeline CI/CD.
{{% /notice %}}

Để nắm vững kiến thức cơ bản về các dịch vụ AWS trước khi thực hành, bạn có thể tham khảo:
  - [Giới thiệu AWS CodeArtifact](https://docs.aws.amazon.com/codeartifact)
  - [Giới thiệu Amazon ECR](https://docs.aws.amazon.com/AmazonECR)
  - [Hướng dẫn GitHub Actions](https://docs.github.com/en/actions)

Trong phần chuẩn bị này, chúng ta sẽ cấu hình môi trường làm việc, bao gồm:
- Tạo **VPC** và **EC2 instance** (tùy chọn, nếu muốn test kết nối private).
- Cài đặt công cụ CLI cần thiết trên máy local hoặc CI/CD runner.
- Tạo **IAM Role** và **Policy** để cấp quyền cho pipeline publish artifact và chạy quét bảo mật.
- Tạo **KMS Key** để mã hóa artifact và log.

---

### **Nội dung chuẩn bị**
- [Cấu hình AWS CLI & Terraform](2.1-configure-cli-terraform/)
- [Tạo IAM Role & Policy cho CI/CD](2.2-create-iam-role/)
- [Khởi tạo CodeArtifact Domain & Repository](2.3-create-codeartifact/)
- [Cài đặt Snyk CLI và cấu hình GitHub Secrets](2.4-configure-snyk/)
