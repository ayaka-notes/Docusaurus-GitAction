# Docusaurus-GitAction
Docusaurus的Git-Action工具，自动化发布到GitPage中。

### 特性
- 自动检测仓库的名称，部署到`username.github.io/<repo-name>`，不需要手动替换配置文件

### 直接使用

```yml
# Simple workflow for deploying static content to GitHub Pages
name: DeployPage

on:
  ####################################################################
  # If you want to setup a cron schedule, uncomment the following line
  # and set the cron schedule as desired (https://crontab.guru/).
  # 
  # 如果你想要设置一个定时任务，取消下面一行的注释，并设置你想要的定时任务
  # 注意：定时任务的时间是 UTC 时间，北京时间需要减去 8 小时

  # schedule:
  #   - cron: '30 4 * * *'


  ####################################################################
  # Allows you to run this workflow manually from the Actions tab
  # 
  # 允许你在 Actions 页面手动运行这个工作流
  workflow_dispatch:
    inputs:
      unconditional-invoking:
        description: 'Deploy Manually'
        type: boolean
        required: true
        default: true
  
  ####################################################################
  # Allows you to run this workflow manually from the Actions tab
  # Runs on pushes targeting the default branch
  # If you think you have enough compute times, or if you deploy just ocassionally
  # you can uncomment the following line
  # 每次推送都自动部署到 GitHub Pages，富哥请务必打开下面的选项。
  # 如果你经常部署你的网站，或者你有足够的计算时间，你可以取消下面一行的注释
  push:
    branches: ["main"]


# Sets permissions of the GITHUB_TOKEN to allow deployment to GitHub Pages
permissions:
  contents: read
  pages: write
  id-token: write

# Allow only one concurrent deployment, skipping runs queued between the run in-progress and latest queued.
# However, do NOT cancel in-progress runs as we want to allow these production deployments to complete.
concurrency:
  group: "pages"
  cancel-in-progress: false

jobs:
  # Single deploy job since we're just deploying
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v3
      - name: DeployPage
        uses: ayaka-notes/Docusaurus-GitPage-Action@v1.1
```
