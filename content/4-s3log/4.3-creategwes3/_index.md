---
title : "Load test pipeline (parallel scan)"
weight : 3
chapter : false
date : 2025-08-12
pre : " <b> 4.3 </b> "
---

{{% notice info %}}
Bước này giúp bạn kiểm tra khả năng chịu tải của pipeline khi thực hiện nhiều tác vụ quét bảo mật song song.
{{% /notice %}}

## Mục tiêu
- Tạo nhiều job quét bảo mật chạy song song
- Đánh giá hiệu năng và thời gian xử lý
- Xác định giới hạn tài nguyên của pipeline

## 1. Chuẩn bị workflow hỗ trợ parallel scan
Mở file `.github/workflows/ci.yml` và chỉnh sửa phần jobs để chạy nhiều luồng quét song song:

```bash
jobs:
  scan:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        service: [service-a, service-b, service-c]
    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Configure AWS credentials
        uses: aws-actions/configure-aws-credentials@v4
        with:
          role-to-assume: ${{ secrets.AWS_ROLE_ARN }}
          aws-region: ap-southeast-1

      - name: Run Snyk scan
        run: snyk test --file=${{ matrix.service }}/package.json --severity-threshold=high
        env:
          SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}
```
# 2. Commit & Push thay đổi
```bash
git add .github/workflows/ci.yml
git commit -m "Enable parallel scanning"
git push origin main
```
## 3. Theo dõi hiệu suất

Mở tab Actions để xem các job chạy song song.

Ghi nhận thời gian hoàn thành pipeline so với khi chạy tuần tự.

Theo dõi log để đảm bảo không có job nào bị timeout.

## 4. Đánh giá kết quả
Nếu thời gian giảm đáng kể và không phát sinh lỗi → cấu hình parallel scan đạt yêu cầu.

Nếu gặp lỗi quá tải (rate limit AWS API hoặc Snyk) → điều chỉnh số luồng trong matrix.