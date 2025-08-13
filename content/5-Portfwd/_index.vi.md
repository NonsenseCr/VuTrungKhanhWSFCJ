---
title : "Cleanup"
weight : 5
chapter : false
date : 2025-08-12
pre : " <b> 5. </b> "
---

{{% notice info %}}
Chúng ta dọn dẹp toàn bộ tài nguyên AWS và GitHub đã tạo trong quá trình workshop để tránh phát sinh chi phí và giữ môi trường làm việc gọn gàng.
{{% /notice %}}

Trong phần này, chúng ta sẽ:
- Xoá CodeArtifact, ECR, KMS, IAM, CloudWatch, SNS, EventBridge, CloudTrail và Audit Manager.
- Xoá các secrets và workflow GitHub liên quan đến workshop.

---

## 1. Xoá CodeArtifact Domain & Repository
1. Vào **AWS Console → CodeArtifact → Repositories**.
2. Chọn repository (dev/test/prod) → **Delete**.
3. Sau khi xoá hết repository, vào **Domains** → xoá domain.

## 2. Xoá ECR Repository (nếu có)
1. Vào **ECR** → chọn repository.
2. Chọn **Delete** để xoá tất cả image và repo.

## 3. Xoá KMS Key
1. Vào **KMS → Customer managed keys**.
2. Chọn key dùng cho artifact/log → **Schedule key deletion**.

## 4. Xoá IAM Role/Policy
1. Vào **IAM → Roles**, chọn role `GitHubActionsPipelineRole` → **Delete**.
2. Vào **IAM → Policies**, xoá policy custom nếu có.

## 5. Xoá CloudWatch Log Group
1. Vào **CloudWatch → Log groups**.
2. Xoá log group `/secure-artifact/pipeline` hoặc các log khác liên quan.

## 6. Xoá SNS Topic & EventBridge Rule
1. Vào **SNS → Topics**, xoá topic `secure-artifact-alert`.
2. Vào **EventBridge → Rules**, xoá rule cảnh báo.

## 7. Xoá CloudTrail & Audit Manager
1. Vào **CloudTrail → Trails**, xoá trail `secure-artifact-trail`.
2. Vào **Audit Manager → Assessments**, xoá assessment `secure-artifact-audit`.

## 8. Xoá GitHub Secrets
1. Mở repository trên GitHub.
2. Vào **Settings → Secrets and variables → Actions**.
3. Xoá các secrets đã thêm cho workshop, ví dụ:
   - `AWS_ACCESS_KEY_ID`
   - `AWS_SECRET_ACCESS_KEY`
   - `AWS_ROLE_ARN`
   - `SNYK_TOKEN`
   - `CODEARTIFACT_REPO_URL`

## 9. Xoá workflow GitHub Actions
1. Mở thư mục `.github/workflows` trong repository.
2. Xoá file workflow, ví dụ: `ci.yml` hoặc các file pipeline khác.
3. Commit thay đổi để xoá workflow khỏi repository.