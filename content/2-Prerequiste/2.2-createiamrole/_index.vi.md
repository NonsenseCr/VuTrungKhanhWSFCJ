---
title : "Tạo IAM Role & Policy cho CI/CD"
weight : 2
chapter : false
date : 2025-08-12
pre : " <b> 2.2 </b> "
---

{{% notice info %}}
Bước này giúp tạo IAM Role trên AWS Console để GitHub Actions có quyền truy cập và thao tác với CodeArtifact, ECR, KMS và các dịch vụ liên quan trong pipeline CI/CD.
{{% /notice %}}

## Mục tiêu
- Tạo IAM Role cho GitHub Actions (OIDC)
- Gán quyền truy cập cần thiết theo nguyên tắc **least privilege**
- Lưu ARN để dùng trong GitHub Secrets

## 1 Tạo OIDC provider cho GitHub (bắt buộc)
- IAM → Identity providers → Add provider → **OpenID Connect (OIDC)**
![VPC](/images/zzz/221.png)
![VPC](/images/zzz/222.png)
![VPC](/images/zzz/223.png)
- Provider URL: `https://token.actions.githubusercontent.com`
- Audience: `sts.amazonaws.com`
- Create

## 2 Tạo IAM Role (Web identity)
- IAM → Roles → Create role → **Web identity**
![VPC](/images/zzz/224.png)

- Identity provider: `token.actions.githubusercontent.com`
- Audience: `sts.amazonaws.com`
- Next → gán các policy cần thiết (CodeArtifact, ECR, KMS, CloudWatch, SNS…) theo nguyên tắc least privilege

## 3. Gán quyền (Policies)
Ở bước **Add permissions**, gán các policy sau:
- `AWSCodeArtifactAdminAccess`
- `AmazonEC2ContainerRegistryFullAccess` (nếu dùng Docker image push lên ECR)
- `AWSKeyManagementServicePowerUser` (quản lý mã hóa KMS)
- `CloudWatchFullAccess` (ghi log, metric)
- `AmazonSNSFullAccess` (gửi cảnh báo)
![VPC](/images/zzz/225.png)

> Bạn có thể tạo **Custom Policy** nếu muốn giới hạn quyền cụ thể.

Bấm **Next**.

## 4. Đặt tên & tạo Role

![VPC](/images/zzz/226.png)

- Review thông tin → **Create role**.

## 5. Lưu ARN Role
Sau khi tạo xong, mở Role vừa tạo và sao chép **Role ARN**.  
![VPC](/images/zzz/227.png)
Role ARN này sẽ dùng để cấu hình trong GitHub Secrets ở bước sau.



