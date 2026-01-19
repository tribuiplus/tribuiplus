## Gitlab

```
Setup Gitlab

Setup Gitlab CI
.gitlab-ci.yml

stages:
  - build
  - test
  - deploy

build_job:
  stage: build
  script:
    - echo "Đang build ứng dụng..."
    - echo "Hoàn tất build!"

test_job:
  stage: test
  script:
    - echo "Chạy test..."
    - sleep 5   # giả lập test mất thời gian
    - echo "Test passed!"

deploy_job:
  stage: deploy
  script:
    - echo "Deploy lên production từ branch $CI_COMMIT_BRANCH"
  environment: production   # theo dõi môi trường trong GitLab

Setup Gitlab runner

Slack Integrations
Repo settings > Slack integraions > Slack notifications
add Webhook
create Slack app > From scratch > add App Name and Channel
setting Incoming Webhooks > Activate Incoming Webhooks and allow Channel
```