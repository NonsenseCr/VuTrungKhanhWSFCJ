---
title : "Chạy full pipeline"
weight : 2
chapter : false
date : 2025-08-12
pre : " <b> 4.2 </b> "
---

{{% notice info %}}
Bước này giúp bạn kiểm tra toàn bộ quy trình pipeline từ khâu build, quét bảo mật cho đến approve hoặc reject artifact.
{{% /notice %}}

## Mục tiêu
- Chạy pipeline với artifact an toàn
- Xác nhận quá trình quét bảo mật
- Artifact được publish thành công khi pass kiểm tra

## 1. Chuẩn bị artifact an toàn
1. Đảm bảo dự án **không** chứa dependency có CVE mức High/Critical.
2. Cập nhật các thư viện lên phiên bản mới nhất:
```bash
npm update
```
3. Kiểm tra thủ công bằng Snyk CLI (tùy chọn):

```bash
snyk test --severity-threshold=high
```

## 2. Commit & Push code

```bash
git add .
git commit -m "Safe build for full pipeline test"
git push origin main
```

## 3. Theo dõi pipeline GitHub Actions
Mở tab Actions trên repository.

Chọn workflow mới chạy.

Quan sát các bước:

Build: cài đặt dependencies, compile code.

Security Scan: chạy Snyk hoặc ECR scan (nếu có container).

Publish: artifact được publish lên CodeArtifact/ECR.

Approve: đánh dấu artifact “Approved” (nếu có bước review thủ công).

## 4. Xác minh kết quả
Artifact xuất hiện trong CodeArtifact/ECR với tag hoặc version mới.

Không có cảnh báo từ SNS/EventBridge.

Log pipeline hiển thị tất cả bước pass thành công.