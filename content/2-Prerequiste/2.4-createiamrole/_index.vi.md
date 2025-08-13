---
title : "Cài đặt công cụ quét Snyk & thiết lập GitHub Secrets"
weight : 4
chapter : false
date : 2025-08-12
pre : " <b> 2.4 </b> "
---


## Mục tiêu
- Cài đặt Snyk CLI trên Windows
- Lấy Snyk Token
- Thêm các thông tin AWS & Snyk vào GitHub Secrets

## 1. Cài đặt Snyk CLI (Windows)
1. Mở PowerShell hoặc Command Prompt.
2. Cài đặt Snyk CLI qua npm (Node.js):
```bash
npm install -g snyk
```
3. Kiểm tra phiên bản:

```bash
snyk --version
```

## 2. Lấy Snyk Token
Đăng ký hoặc đăng nhập tại: https://snyk.io

Truy cập Account settings.

Sao chép Auth token của bạn.

![VPC](/images/zzz/241.png)
## 3. Cấu hình GitHub Secrets
Mở GitHub Repository của dự án.

Vào Settings → Secrets and variables → Actions.
![VPC](/images/zzz/242.png)
Thêm các secrets sau:

AWS_ACCESS_KEY_ID = Access key của IAM user/role

AWS_SECRET_ACCESS_KEY = Secret key của IAM user/role

AWS_ROLE_ARN = ARN của IAM Role (nếu dùng OIDC)

CODEARTIFACT_REPO_URL = Chuỗi lấy được ở bước cuối mục 2.3

SNYK_TOKEN = Token lấy ở bước 2

![VPC](/images/zzz/243.png)

## 4. Xác thực Snyk CLI (tuỳ chọn)

Bạn có thể xác thực Snyk CLI trên máy local để test:

```bash
snyk auth <SNYK_TOKEN>
```