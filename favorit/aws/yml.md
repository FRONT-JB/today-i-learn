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

**`Turborepo Actions`**

```yml
name: Condition Monorepo Build

on:
  pull_request:
    branches:
      - main

jobs:
  condition:
    name: Find Turborepo Cache Build
    runs-on: ubuntu-latest
    timeout-minutes: 10
    steps:
      - uses: actions/checkout@v2
        with:
          fetch-depth: 100
      - uses: actions/setup-node@v2-beta
        with:
          node-version: "16.14.x"
          check-latest: true

      - name: Turbo Cache
        id: turbo-cache
        uses: actions/cache@v2
        with:
          path: .turbo
          key: turbo-${{ github.job }}-${{ github.ref_name }}-${{ github.sha }}
          restore-keys: |
            turbo-${{ github.job }}-${{ github.ref_name }}-

      - uses: c-hive/gha-yarn-cache@v2

      - name: Install Dependencies
        run: yarn install

      - uses: marceloprado/has-changed-path@v1
        id: service-one
        with:
          paths: apps/service-one

      - uses: marceloprado/has-changed-path@v1
        id: service-two
        with:
          paths: apps/service-two

      - uses: marceloprado/has-changed-path@v1
        id: service-three
        with:
          paths: apps/service-three

      - uses: marceloprado/has-changed-path@v1
        id: service-four
        with:
          paths: apps/service-four

      - name: Build Test Service One
        if: steps.serivce-one.outputs.changed == 'true'
        run: yarn build:service-one

      - name: Build Test Service Two
        if: steps.service-two.outputs.changed == 'true'
        run: yarn build:service-two

      - name: Build Test Service Three
        if: steps.service-three.outputs.changed == 'true'
        run: yarn build:service-three

      - name: Build Test Service Four
        if: steps.service-four.outputs.changed == 'true'
        run: yarn build:service-four
```
