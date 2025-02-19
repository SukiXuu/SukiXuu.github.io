---
author: "Suki Xuu"
title: "个人网站搭建4 --AWS CDN"
date: "2025-01-21"
description: "使用AWS CDN加速github pages个人网站"
cntags: ["Web Build", "CDN", "AWS"]
ShowToc: true
ShowBreadCrumbs: false
---

使用AWS CDN加速github pages个人网站。

<!--more-->
### 1. 不更改文件存储位置，只创建 CDN 分发
CDN Content Delivery Network（内容分发网络）是一种基于网络的服务，它利用各地的服务器之间互联互通的特性，通过在用户访问网站时自动选择最佳的服务器提供内容，提高网站的访问速度。

AWS 的 CDN 服务叫做 CloudFront



#### 测试访问速度
[dotcom DNS测试网站](https://www.dotcom-tools.com/dns-trace-test)

![](/assets/images/dns_test_0.png)

#### 配置AWS CloudFront
1. 为个人域名申请一个公有证书：
	- 登录 AWS 管理控制台，选择 `Certificate Manager` -> `Request a certificate`
	- 输入您的域名，选择 `DNS validation` 方法，然后点击 `Next`
	- 创建一个域名Record，添加生成的CNAME记录，进行验证. 
		**注意原本域名上的CNAME记录需要删除，不然会导致验证失败;关联来自 AWS Certificate Manager 的证书。证书必须位于美国东部(弗吉尼亚北部)区域(us-east-1)。**
2. 创建一个新的 CloudFront 分配
3. Origin domain -- 输入您的 Github Pages 仓库的**域名**，如：`https://sukixuu.github.io`
4. 备用域名(CNAME) –- 添加您的域名，如：`sukixuu.click` (可选, 需要申请公有证书)

![](/assets/images/dns_test_1.png)

#### 让 Github Actions 在每次有文件更改后自动初始化 CloudFront
1. 在工作流中添加一个 `AWS CLI` 任务，安装最新版本的 AWS CLI
	```yml
	- name: Set up AWS CLI
      uses: aws-actions/configure-aws-credentials@v1
      with:
        aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
        aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
        aws-region: 'us-east-1'  # 替换为您所在的 AWS 区域
	```
      - 在AWS IAM中创建用户，并赋予其 `AmazonCloudFrontFullAccess` 和 `AmazonS3FullAccess` 权限。
      - 对此用户申请 Access Key 和 Secret Key。
      - 在GitHub Secrets中 **repository secrets** 添加 `AWS_ACCESS_KEY_ID` 和 `AWS_SECRET_ACCESS_KEY`，并将其设置为您的 IAM 用户的 Access Key 和 Secret Key。

2. 在工作流中添加一个 `AWS CloudFront` 任务，用于初始化 CloudFront
	```yml
    - name: Invalidate CloudFront Cache
      run: |
        aws cloudfront create-invalidation \
          --distribution-id YOUR_CLOUDFRONT_DIST_ID \ # 替换为您的 CloudFront 分配 ID
          --paths "/*" # 可以指定需要刷新的文件路径，这里全部刷新
	```



---


---

### 构建站点-本地
1. 创建 Hugo 项目
	```sh
	hugo new site --format yaml
	hugo new site /Users/sukixuu/Desktop/SukiBlog --format yaml   #指定路径
	```

2. 进入项目目录并添加主题
	```sh
	cd /Users/sukixuu/Desktop/SukiBlog    #进入目录
	```
	- [Theme](https://themes.gohugo.io/)选择，根据文档安装；这里使用[PaperMod](https://github.com/adityatelange/hugo-PaperMod)
		```sh
		git init
		```
		下载：
		```sh
		git submodule add --depth=1 https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod
		git submodule update --init --recursive # needed when you reclone your repo (submodules may not get cloned automatically)
		```
		更新（以后更新使用）：
		```sh
		git submodule update --remote --merge
		```

3. 将网站配置中的主题设置为PaperMod
   在 `hugo.yaml` 中添加以下，并重新命名成为 `config.yaml`：
	```yaml
	theme: ["PaperMod"]
	```

4. 启动 Hugo 服务器
	```sh
	hugo server
	```

---

