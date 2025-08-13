---
title : "Thiết lập Audit Manager & CloudTrail"
weight : 3
chapter : false
date : 2025-08-12
pre : " <b> 3.3 </b> "
---

{{% notice info %}}
Bước này giúp bạn bật CloudTrail để ghi lại toàn bộ hoạt động trên tài khoản AWS và cấu hình Audit Manager để thu thập log phục vụ kiểm tra bảo mật và tuân thủ.
{{% /notice %}}

## Mục tiêu
- Bật và cấu hình AWS CloudTrail
- Tạo trail ghi log vào S3 và CloudWatch
- Kích hoạt Audit Manager để thu thập log tự động

## 1. Bật CloudTrail
1. Đăng nhập **AWS Console** → vào **CloudTrail**.
2. Chọn **Create trail**.
3. Nhập tên, ví dụ: `secure-artifact-trail`.
4. Chọn **Apply trail to all regions** để ghi log trên toàn bộ khu vực.
5. Ở **Storage location**, tạo mới hoặc chọn S3 bucket hiện có.
6. (Tuỳ chọn) Bật **CloudWatch Logs** để gửi log song song vào CloudWatch.
7. Bấm **Create trail**.

## 2. Kiểm tra CloudTrail hoạt động
- Thực hiện một hành động trên AWS Console (ví dụ: xem thông tin repository CodeArtifact).
- Vào CloudTrail → **Event history** → tìm sự kiện vừa tạo để xác nhận.

## 3. Bật AWS Audit Manager
1. Vào dịch vụ **Audit Manager**.
2. Bấm **Get started** nếu là lần đầu sử dụng.
3. Chọn **Create assessment**:
   - Name: `secure-artifact-audit`
   - S3 bucket lưu evidence: tạo mới hoặc chọn bucket hiện có.
4. Chọn các dịch vụ cần giám sát (CodeArtifact, ECR, IAM, CloudWatch...).
5. Hoàn tất để Audit Manager bắt đầu thu thập log và evidence.

## 4. Kiểm tra dữ liệu Audit
- Mở assessment vừa tạo, vào tab **Evidence** để xem log và sự kiện đã thu thập từ CloudTrail.

