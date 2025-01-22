---
author: "Suki Xuu"
title: "个人网站搭建2 --git"
date: "2025-01-21"
description: "使用HUGO搭建个人网站"
cntags: ["Web Build", "Git"]
ShowToc: false
ShowBreadCrumbs: false
---

使用HUGO搭建个人网站。

<!--more-->
### 把本地托管到GitHub
1. 本地terminal中cd到HUGO项目目录
2. 将本地repo初始化为一个新的repo
   ```bash
   echo "# SukiXuu.github.io" >> README.md
   git init
   ```
3. 暂存所有文件，commit到本地仓库
    ```bash
    git add.
    #Adds the files in the local repository and stages them for commit. 若要取消暂存文件，请使用
    # `git reset --hard HEAD^` 撤销最后一次提交, 不保留任何提交
	# `git reset --soft HEAD^` 撤销最后一次提交，保留提交记录到暂存区
   ```

   ```bash
   git commit -m "First Commit"
   ```

4. 关联远程仓库：
   ```bash
   git branch -M main
   git remote add origin https://github.com/SukiXuu/SukiXuu.github.io
   ```
5. 把本地仓库推送到远程仓库：
   ```
   git push -u origin main
   ```
6. 等待几分钟，网站应该就已经部署成功了。


---


---

