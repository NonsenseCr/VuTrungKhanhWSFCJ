---
title : "4.5 – Xuất báo cáo"
weight : 5
chapter : false
date : 2025-08-12
pre : " <b> 4.5 </b> "
---

{{% notice info %}}
Bước này giúp bạn tổng hợp kết quả thực hành, bao gồm log pipeline, kết quả quét bảo mật và các cảnh báo, nhằm tạo báo cáo hoàn chỉnh cho workshop.
{{% /notice %}}

## Mục tiêu
- Thu thập log và kết quả từ GitHub Actions
- Lưu trữ báo cáo quét bảo mật từ Snyk và ECR
- Tổng hợp thành báo cáo cuối cùng

## 1. Thu thập log pipeline
1. Mở repository trên GitHub.
2. Vào tab **Actions** → chọn workflow cần xuất báo cáo.
3. Bấm **Download logs** để tải toàn bộ log chạy pipeline.

## 2. Lưu kết quả quét bảo mật
- **Snyk**: Trong bước scan của pipeline, lưu output dưới dạng file JSON hoặc HTML (sử dụng `--json` hoặc `--json-file-output`).
```bash
snyk test --severity-threshold=high --json-file-output=report.json
```
ECR Enhanced Scanning: Vào AWS Console → ECR → chọn image → Scan results → Export kết quả (copy/paste hoặc screenshot).

## 3. Ghi nhận cảnh báo
Mở email hoặc Slack để lấy nội dung cảnh báo từ SNS/EventBridge (nếu có).

Lưu lại thông tin về thời gian, loại sự kiện, mức độ.

## 4. Tổng hợp báo cáo
Tạo file workshop-report.md hoặc workshop-report.pdf với nội dung:

Mô tả hạ tầng và pipeline đã triển khai.

Kết quả quét bảo mật (pass/fail).

Các cảnh báo và xử lý.

Bài học rút ra và đề xuất cải tiến.

## 5. Lưu trữ và chia sẻ
Lưu báo cáo trong repository (thư mục reports/) hoặc trên S3.
