---
title : "Cấu hình môi trường CLI (AWS CLI & Terraform)"
weight : 1
chapter : false
date : 2025-08-12
pre : " <b> 2.1 </b> "
---


##  Mục tiêu
- Cài đặt AWS CLI v2 trên Windows
- Cài đặt Terraform ≥ v1.5 trên Windows
- Kiểm tra kết nối AWS

## 1. Cài đặt AWS CLI v2 (Windows)
**a) Trên máy tính (CLI):**
1. Tải bộ cài tại: https://awscli.amazonaws.com/AWSCLIV2.msi  
2. Chạy file `.msi` và cài đặt như phần mềm thông thường.
3. Sau khi cài đặt, mở **Command Prompt** hoặc **PowerShell** và kiểm tra:
```bash
aws --version
```
**b) Trên web console:**

AWS Console không cần cài CLI. Tuy nhiên, khi cần thao tác nhanh, bạn có thể dùng AWS CloudShell trực tiếp trên giao diện web (icon terminal góc trên bên phải Console) để chạy các lệnh AWS CLI mà không cần cài đặt gì thêm.
![VPC](/images/zzz/211.png)

## 2. Cấu hình AWS CLI
**2.1) Trên web console:**
Vào IAM > Users, chọn user của bạn , nếu chưa thì tạo mới.

![VPC](/images/zzz/213.png)

Nhập tên như bình thường , sau đó chọn quyền hạn như sau.

![VPC](/images/zzz/214.png)

Next tiếp, sau đó chọn user vừa tạo. Chọn Security credentials > Create access key để tạo Access Key phục vụ aws configure.

![VPC](/images/zzz/215.png)
![VPC](/images/zzz/216.png)

Chọn CLI.

![VPC](/images/zzz/217.png)

Tạo thành công như hình, ta copy 2 key như trên màn hình lại. 

![VPC](/images/zzz/218.png)



**2.2) Trên máy tính (CLI):**
Điền Access Key, Secret Key, Region và output format. 

Mở PowerShell.

```bash
aws configure
```

Sau đó điền lần lượt 2 key bạn vừa tạo vào như sau(tham khảo):
![VPC](/images/zzz/212.png)

Với Region bạn tự quyết định nhé !

## 3. Cài đặt Terraform ≥ v1.5

Tải từ: https://developer.hashicorp.com/terraform/downloads
Giải nén và thêm vào hệ thống `PATH`

Sau khi tải xong ta tìm View advanced system settings
![VPC](/images/zzz/219.png)

Follow cac bước sau để add `PATH`
![VPC](/images/zzz/2110.png)

Kiểm tra:

```bash
terraform -version
```

## 4. Kiểm tra kết nối AWS 

**a) CLI:**

```bash
aws sts get-caller-identity
```
Nếu trả về thông tin account/user là đã cấu hình thành công.

**b) Console:**

Đăng nhập vào AWS Console, kiểm tra góc phải hiển thị đúng account và region.