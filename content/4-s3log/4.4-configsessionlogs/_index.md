---
title : "Failover test (simulate outage)"
weight : 4
chapter : false
date : 2025-08-12
pre : " <b> 4.4 </b> "
---

{{% notice info %}}
Bước này giúp bạn mô phỏng sự cố dịch vụ (CodeArtifact hoặc ECR) để kiểm tra cơ chế failover và khả năng phục hồi của pipeline.
{{% /notice %}}

## Mục tiêu
- Mô phỏng tình huống dịch vụ artifact bị gián đoạn
- Đánh giá thời gian phát hiện và phục hồi
- Kiểm tra các bước fallback đã cấu hình

## 1. Mô phỏng sự cố CodeArtifact/ECR
### Cách 1 – Thay đổi tạm thời endpoint
- Vào file cấu hình pipeline, thay đổi **CODEARTIFACT_REPO_URL** hoặc endpoint ECR thành giá trị sai.
- Điều này sẽ làm bước publish artifact thất bại.

### Cách 2 – Tạm thời vô hiệu hóa quyền truy cập
- Vào **IAM Console**, edit role của GitHub Actions và remove quyền publish/download.
- Lưu thay đổi để pipeline mất quyền truy cập.

## 2. Chạy pipeline
- Commit và push thay đổi nhỏ để kích hoạt workflow.
- Quan sát pipeline fail ở bước publish.

## 3. Xác minh cơ chế fallback
- Nếu đã cấu hình multi-region hoặc repository dự phòng, kiểm tra pipeline tự động chuyển sang endpoint khác.
- Nếu có script retry, xác minh số lần retry và thời gian chờ.

## 4. Khôi phục cấu hình
- Trả lại endpoint và quyền truy cập ban đầu.
- Chạy lại pipeline để đảm bảo hoạt động bình thường.

