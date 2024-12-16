---
author: ["Michael Wu"]
title: "如何简单快速搭建你的个人博客"
date: "2024-12-16"
description: "一站式解决搭建博客时遇到的问题，完成从创建项目到谷歌收录的流程"
summary: "一站式解决搭建博客时遇到的问题，完成从创建项目到谷歌收录的流程"
tags: ["blog", "papermod", "google", "hugo"]
categories: ["themes", "syntax"]
series: ["Blog Guide"]
ShowToc: true
TocOpen: true
---
### 写在开头

- 都点进这篇了，一定是想要搭建自己的博客。
- 如果你和我一样，对前端一窍不通，也不想在博客里整太多花哨效果，只希望有尽量简单浓缩的功能，那可以和我一样使用Hugo。
- 如果你去咨询程序猿朋友或者各种论坛，在中午互联网上大家基本都会推荐hexo，这个开源项目教程完善，插件多，并且重要的是**中文支持好**
- 但为什么还是推荐hugo呢？因为它快，它的自动部署非常快，同时其实框架完善程度不比hexo差，同时我也比较喜欢papermod这个主题的风格。
- <del>当然不是因为我随便在github找到了这个<del>
- 如果你想搞得炫酷些我其实推荐你出门右转hexo，否则你可以直接按住我下面的一步一步依次完成，很快就能完成整个博客的配置部署
- 没有代码需求，不要求会懂得任何前端知识甚至不要求懂代码，纯宝宝巴士难度
##### 注：本文全程只在Windows系统下操作，Linux系统的也可以参考，但出什么额外问题还请自行搜索解决

### 步骤1：项目搭建

- 首先点进[Hugo](https://github.com/gohugoio/hugo/releases/tag/v0.139.4)，下载符合的包。如果你是windows系统，一般是下载这个[链接](https://github.com/gohugoio/hugo/releases/download/v0.139.4/hugo_extended_0.139.4_windows-amd64.zip)
- 下载下来的压缩包位置无所谓，自己找地方解压。解压完之后有个exe，不需要点击它。
- 添加环境变量：
  - 直接按win键，找到搜索，搜索**环境变量**
  - 点进环境变量
  ![图片](images/blog_1.png)
  - 在用户变量中，找到Path，点击编辑
  ![图片](images/blog_2.png)
  - 新建一条，这里请找到你自己解压hugo的位置并粘贴进来
  ![图片](images/blog_3.png)
  - 配置完毕！
- 创建项目
  - 这里推荐用vscode了，vscode完美符合我们需要的快捷省事
  - vscode自带版本管理，但请提前安好git。怎么安装git请自行搜索。vscode需要中文的话请自行搜索。
  - 在vscode中呼出终端
  ![图片](images/blog_4.png)
  - 在终端中输入：

    ```{hl_lines=[2,8]}
    hugo new site 你的博客名称 --format yaml
    ```

  - 一般情况下文件夹会创建到C盘。如果你创建失败，检查你hugo环境变量有没有配置正确
  - 这个文件夹就是你的博客项目了，以后写博客，修改网页都在这里面弄
  - 在vscode中打开【文件】-【打开文件夹】，选择刚刚这个博客项目文件夹
- 安装PaperMod主题
  - 如果你什么都不懂，推荐先跟着我来，安个PaperMod试试，以后熟练了可以换你喜欢的别的主题或者安插件什么的
  - [下载主题](https://github.com/adityatelange/hugo-PaperMod/archive/refs/tags/v8.0.zip)完成后请解压，并改名hugo-PaperMod-8.0为PaperMod。将这个文件夹移动到博客项目文件夹中themes文件夹下
  ![图片](images/blog_5.png)
  - 注：虽然官方推荐使用子模块，但实话实说并没有什么同步主题那边的更新的必要，为了避免不必要的报错浪费时间，我觉得还不如直接下载下来，或者git clone之后删除.git文件夹
- 完成项目搭建！

### 步骤2：修修改改

- 首先，如果你不知道怎么写配置文件，直接复制我仓库首页的hugo.yaml文件中的内容即可，粘贴到你博客目录下的hugo.yaml中。根据你自己的情况做更改。
- 推荐先下载papermod仓库里的[exampleSite](https://github.com/adityatelange/hugo-PaperMod/tree/exampleSite)，下载zip压缩包即可，把其中的assets、content中的内容直接复制到你的项目相同名称目录下
- 为了让你每次推送新内容后自动构建并更新网站，推荐使用github workflow。
  - 在博客项目文件夹中创建以下目录：**你的博客/.github/workflows/hugo.yaml**
  - 注意不要漏掉那个'.'
  - 在这个新创建的hugo.yaml文件中复制粘贴以下内容
  ```{hl_lines=[2,8]}
  # Sample workflow for building and deploying a Hugo site to GitHub Pages
  name: Deploy Hugo site to Pages

  on:
    # Runs on pushes targeting the default branch
    push:
      branches:
        - main

    # Allows you to run this workflow manually from the Actions tab
    workflow_dispatch:

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

  # Default to bash
  defaults:
    run:
      shell: bash

  jobs:
    # Build job
    build:
      runs-on: ubuntu-latest
      env:
        HUGO_VERSION: 0.137.1
      steps:
        - name: Install Hugo CLI
          run: |
            wget -O ${{ runner.temp }}/hugo.deb https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_extended_${HUGO_VERSION}_linux-amd64.deb \
            && sudo dpkg -i ${{ runner.temp }}/hugo.deb          
        - name: Install Dart Sass
          run: sudo snap install dart-sass
        - name: Checkout
          uses: actions/checkout@v4
          with:
            submodules: recursive
            fetch-depth: 0
        - name: Setup Pages
          id: pages
          uses: actions/configure-pages@v5
        - name: Install Node.js dependencies
          run: "[[ -f package-lock.json || -f npm-shrinkwrap.json ]] && npm ci || true"
        - name: Build with Hugo
          env:
            HUGO_CACHEDIR: ${{ runner.temp }}/hugo_cache
            HUGO_ENVIRONMENT: production
            TZ: America/Los_Angeles
          run: |
            hugo \
              --gc \
              --minify \
              --baseURL "${{ steps.pages.outputs.base_url }}/"          
        - name: Upload artifact
          uses: actions/upload-pages-artifact@v3
          with:
            path: ./public

    # Deployment job
    deploy:
      environment:
        name: github-pages
        url: ${{ steps.deployment.outputs.page_url }}
      runs-on: ubuntu-latest
      needs: build
      steps:
        - name: Deploy to GitHub Pages
          id: deployment
          uses: actions/deploy-pages@v4
  ```
  - 完成！以后你只需要推送到github即可放手不管，等待其自动部署即可
- 远程仓库与推送：
  - 既然要用静态网站来搭建博客，自然是要托管到别的地方。这样就能做到不租用服务器就能免费获得博客网站。
  - 这里使用github pages演示。这是最流行的静态博客托管方案之一，缺点是都是.github.io结尾，无法被百度收录。但可以用谷歌收录。有关收录和搜索相关，写在本文后面。
  - 首先，在你的github创建一个新仓库，注意！**仓库名称必须是：你的github名字.github.io**，创建仓库时左边owner就会显示你的github名字，照着输入就行
  ![图片](images/blog_6.png)
  - 创建完空仓库后，找到你仓库的https地址或ssh Key，复制
  - 回到vscode，在侧边栏中找到源代码管理，点击初始化仓库。
  - 现在仓库还没有连接到你的github远程仓库，请按照下面图片，找到添加远程仓库
  ![图片](images/blog_7.png)
  - 注：配置github账号请自行搜索“本地Git配置远程Github账户”
  - 添加完成远程仓库后，vscode会自动尝试同步一下远程仓库，这里就可以验证你当前网络是不是可以访问你的远程仓库。
  - 推荐现在先在终端输入
  ```{hl_lines=[2,8]}
    git add .
  ```
  - 这是为了确保所有文件都被推送上去。
  - 确认无误后，随便输入点什么，点击提交。直接暂存所有并提交即可。
  - 这个时候，理论上现在会出现一个按钮，这个按钮提示**创建一个Branch**，点击。请确保是创建main。
  - 然后，如果一切顺利，你的远程仓库就会有内容了，main分支下有博客文件
  - 如果你前面是照着我做的，现在可以点击**Action**查看远程工作流运行情况，等待其成功部署后，在浏览器输入仓库名作为网址，应该可以打开查看到内容了！
- 完成以上，以后写博客就在content/posts下创建.md文件，写markdown即可。每次希望同步到远程仓库时，可以类似地提交、同步即可。 

### 步骤3：搜索引擎支持

- 这里只介绍google的操作流程。
- 为了支持google收录，你需要创建这个文件：layouts/_internal/google_analytics.html。请在相应目录创建google_analytics.html
- 现在先不管它，去google试试：
![图片](images/blog_8.png)
- 大概率你会搜不到你的博客网站，这是因为google没有收录。这里介绍最简单的方法：[谷歌分析](https://analytics.google.com/analytics/web/#/provision)。
- 进入网站后，填写一些信息，把你的博客网址填上去，它会生成一个G开头的衡量ID，复制这个ID号，替换到**博客根目录/hugo.yaml**中，如图所示
![图片](images/blog_9.png)
![图片](images/blog_10.png)
- 刚刚创建的google_analytics.html中，粘贴以下内容：
  
```html
<!-- Google tag (gtag.js) -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-你的ID"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());

  gtag('config', 'G-你的ID');
</script>
```

- 提交并推送
- 等待github那边部署完成后，回到谷歌分析网站，看看是不是已经成功计入分析了
- 重复一遍在google搜索site:你的网址，如图所示
![图片](images/blog_8.png)
- 点进**尝试使用 Google Search Console**
- 如果刚刚你的google分析成功了，这里应该会让你自动选择使用谷歌分析认证
- 完成认证后，理论上一两天后你就可以在google上搜到你的网站了。这里同时推荐在Search Console里的站点地图中添加一下你的网站sitemap，这是为了方便google抓取你博客文章，让更多人容易搜索到你的文章
  - sitemap.xml在配置正确的情况下会自动生成，只需要输入sitemap.xml即可。类似这样：
  ![图片](images/blog_11.png)
  - 提交。这个站点地图需要等待相当久，过一周来看都可以。
- 这样就完成了所需要的所有基本的谷歌设置。

### 待更新：GoogleAD接入，百度收录等