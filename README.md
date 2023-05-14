# circleci-deploy
https://github.com/3Kmfi6HP/argo-airport-paas

部署成功示例

![image](https://github.com/3Kmfi6HP/circleci-deploy/assets/58669916/97f46380-021d-43fc-966f-d7702dbd0a07)

每10分钟会自动停止，重新部署方法。

## 使用方法
```Dashboard --> https://app.circleci.com/pipelines/gh/名字/仓库名称 --> Project Settings --> Triggers --> Add Trigger --> Repeats Per Hour* 设置 10min ```

```yaml
# Use the latest 2.1 version of CircleCI pipeline process engine.
# See: https://circleci.com/docs/2.0/configuration-reference
version: 2.1

# Define a job to be invoked later in a workflow.
# See: https://circleci.com/docs/2.0/configuration-reference/#jobs
jobs:
  test:
    # Specify the execution environment. You can specify an image from Dockerhub or use one of our Convenience Images from CircleCI's Developer Hub.
    # See: https://circleci.com/docs/2.0/configuration-reference/#docker-machine-macos-windows-executor
    docker:
      - image: ghcr.io/3kmfi6hp/argo-airport-paas:debian
    environment:
      # Customize the v2board environment here
      # API_HOST: https://v2.circleci-dev.example.com
      # API_KEY: xxxx
      # NODE_ID: 55
      # Customize the argo environment here
      ARGO_DOMAIN: circleci-dev.example.com
      ARGO_AUTH: xxx
      TUNNEL_TRANSPORT_PROTOCOL: http2
      # Customize the nezha environment here
      # NEZHA_KEY: xxxx
      # NEZHA_PORT: 555
      # NEZHA_SERVER: nz-circleci-dev.example.com
    # Add steps to the job
    # See: https://circleci.com/docs/2.0/configuration-reference/#steps
    working_directory: /app
    steps:
      - run:
          name: Run service
          command: node server.js & pm2 logs
# Invoke jobs via workflows
# See: https://circleci.com/docs/2.0/configuration-reference/#workflows
workflows:
  orb-free-workflow:
    jobs:
      - test
```
