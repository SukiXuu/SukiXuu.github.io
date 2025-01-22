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
    # `git remote remove origin` 移除已有的远程仓库origin
    ```
5. 把本地仓库推送到远程仓库：
    ```
    git push -u origin main
    ```

---

6. 更改GitHub Actions的配置文件，使其能够自动部署网站。
    - settings -> actions -> new workflow -> set up a workflow yourself -> 选择HUGO模板 -> 编辑yaml文件 -> 找到push到main分支的步骤 -> 找到deploy步骤 -> 编辑deploy步骤，对比[PaperMod Demo 的 部署文件](https://github.com/adityatelange/hugo-PaperMod/actions/runs/9920318194/workflow)，自行做相应修改。
    - 保存并运行workflow。
    - 等待几分钟，网站应该已经部署成功。在之后的github提交会自动部署到网站。


---
.gitignore文件:
```
# Compiled Object files, Static and Dynamic libs (Shared Objects)
*.o
*.a
*.so

# Folders
_obj
_test

# Architecture specific extensions/prefixes
*.[568vq]
[568vq].out

*.cgo1.go
*.cgo2.c
_cgo_defun.c
_cgo_gotypes.go
_cgo_export.*

_testmain.go

*.exe
*.test

/public
.DS_Store
.hugo_build.lock
# resources/_gen/
```

---

