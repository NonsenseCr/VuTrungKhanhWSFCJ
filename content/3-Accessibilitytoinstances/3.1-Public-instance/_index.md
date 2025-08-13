---
title : "Tạo CloudWatch Log Group & Metric Filter"
weight : 1
chapter : false
date : 2025-08-12
pre : " <b> 3.1 </b> "
---

## Mục tiêu
- Tạo CloudWatch Log Group để lưu log
- Liên kết log từ CodeArtifact/ECR vào CloudWatch
- Tạo Metric Filter để phát hiện lỗi hoặc sự kiện quan trọng

## 1. Tạo Log Group
1. Đăng nhập **AWS Console** → vào **CloudWatch**.
2. Chọn **Logs → Log groups** → **Create log group**.
3. Nhập tên, ví dụ: `/secure-artifact/pipeline`.
4. Chọn **Retention** (ví dụ: 30 ngày).
5. Bấm **Create**.

## 2. Kết nối log từ dịch vụ
- **CodeArtifact**: Vào CodeArtifact → Settings → Enable CloudWatch logs (nếu hỗ trợ).
- **ECR**: Mặc định Enhanced Scanning gửi kết quả vào EventBridge, bạn có thể tạo rule gửi log vào CloudWatch.
- **GitHub Actions**: Có thể cấu hình pipeline gửi log ra CloudWatch qua AWS CLI hoặc Lambda tùy chọn.

## 3. Tạo Metric Filter
1. Trong **Log group** vừa tạo, chọn **Create metric filter**.
2. Chọn log stream và nhập **Filter pattern**, ví dụ:
```bash
?ERROR ?Exception
```
3. Đặt tên metric, ví dụ: PipelineErrorCount.

4. Chọn namespace, ví dụ: SecureArtifact.

5. Bấm Create filter.

## 4. Xác minh
Gây thử một lỗi trong pipeline để log được ghi.

Kiểm tra metric filter đã nhận sự kiện.