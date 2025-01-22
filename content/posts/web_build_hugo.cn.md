---
author: "Suki Xuu"
title: "个人网站搭建1 --Hugo"
date: "2025-01-21"
description: "使用HUGO搭建个人网站"
cntags: ["Web Build", "Hugo"]
ShowToc: true
ShowBreadCrumbs: false
---

使用HUGO搭建个人网站。

<!--more-->
### Requirements
#### [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
#### [Go](https://go.dev/doc/install)
1. 安装golong版本管理工具
   - Install [Bison](https://www.gnu.org/software/bison/):  
	```sh
	bison --version    #测试是否已经安装
	brew install bison
	```
	
   - Install [gvm](https://github.com/moovweb/gvm?tab=readme-ov-file): 
    ```sh
    bash < <(curl -s -S -L https://raw.githubusercontent.com/moovweb/gvm/master/binscripts/gvm-installer)
    ```
    
2. 使用gvm下载go：
	```sh
	brew install go@1.22    #gvm需要先拥有一个go
	gvm install go1.23
	gvm use go1.23    #default
	```

#### [Dart Sass](https://gohugo.io/hugo-pipes/transpile-sass-to-css/#dart-sass)
  使用 Sass 语言的最新功能时，需要 Dart Sass 将 Sass 转译为 CSS。
```sh
brew install sass/sass/sass
```

---

### HUGO下载
extended/deploy editions：可以将您的网站直接部署到 Google Cloud Storage 存储桶、AWS S3 存储桶或 Azure 存储容器。查看[详细信息](https://gohugo.io/hosting-and-deployment/hugo-deploy/)。
1. Install a C compiler, either [GCC](https://gcc.gnu.org/) or [Clang](https://clang.llvm.org/) 二选一
	```sh
	gcc --version    #check gcc是否安装
	clang --version    #check clang是否安装
	```
2. To build the extended/deploy edition:
	```sh
	CGO_ENABLED=1 go install -tags extended,withdeploy github.com/gohugoio/hugo@latest
	```

	```sh
	hugo version    #check
	```

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

