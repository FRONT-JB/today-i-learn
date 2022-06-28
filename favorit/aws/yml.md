# Github Actions YML

**`Deploy Actions`**

```yml
name: DEPLOY

on:
  workflow_dispatch:
    inputs:
      name:
        type: choice
        description: "Author"
        options:
          - Option1
          - Option2
          - Option3
        required: true
      message:
        description: "Build History"
        required: true

jobs:
  build:
    name: Build
    runs-on: ubuntu-latest
    steps:
      - name: executing remote ssh commands using key
        uses: appleboy/ssh-action@master
        with:
          host: ${{ secrets.EC2HOST }}
          username: ${{ secrets.EC2USERNAME }}
          key: ${{ secrets.EC2PEMKEY }}
          script: |
            # Build Shell
            ~/deploy.sh
      # 빌드 성공 메세지 발송
      - name: Send Build Success Message
        uses: appleboy/telegram-action@master
        if: success()
        with:
          to: ${{ secrets.TELEGRAM_CHAT_ID }}
          token: ${{ secrets.TELEGRAM_TOKEN }}
          format: markdown
          message: |
            Author: ${{ github.event.inputs.name }}
            Status: 👍 **Success**
            Build Message: ${{ github.event.inputs.message }}
            [See Action Log](https://github.com/${{ github.repository }}/actions)
      # 빌드 실패 메세지 발송
      - name: Send Build Success Message
        uses: appleboy/telegram-action@master
        if: failure()
        with:
          to: ${{ secrets.TELEGRAM_CHAT_ID }}
          token: ${{ secrets.TELEGRAM_TOKEN }}
          format: markdown
          message: |
            Author: ${{ github.event.inputs.name }}
            Status: 🔥 **Failure**
            Build Message: ${{ github.event.inputs.message }}
            [See Action Log](https://github.com/${{ github.repository }}/actions)
```
