---
author: "Suki Xuu"
title: "个人网站搭建2 --git"
date: "2025-01-22"
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
    在本地创建一个`.gitignore`文件，内容如下：
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

    然后执行：
    ```bash
    echo "# SukiXuu.github.io" >> README.md    # 创建README.md文件
    git init   # 初始化本地仓库，在hugo安装submodule时已经初始化过了，这里不用再初始化
    ```

3. 暂存所有文件，commit到本地仓库
    ```bash
    git add.
    # Adds the files in the local repository and stages them for commit. 若要取消暂存文件，请使用
    # `git reset --hard HEAD^` 撤销最后一次提交, 不保留任何提交
	# `git reset --soft HEAD^` 撤销最后一次提交，保留提交记录到暂存区
    ```

    ```bash
    git commit -m "First Commit"
    ```

1. 关联远程仓库：
    ```bash
    git branch -M main
    git remote add origin https://github.com/SukiXuu/SukiXuu.github.io
    # `git remote remove origin` 移除已有的远程仓库origin
    ```
2. 把本地仓库推送到远程仓库：
    ```bash
    git push -u origin main
    ```

---

6. 更改GitHub Actions的配置文件，使其能够自动部署网站。
    - settings -> actions -> new workflow -> set up a workflow yourself -> 选择HUGO模板 -> 编辑yaml文件 -> 找到push到main分支的步骤 -> 找到deploy步骤 -> 编辑deploy步骤，对比[PaperMod Demo 的 部署文件](https://github.com/adityatelange/hugo-PaperMod/actions/runs/9920318194/workflow)，自行做相应修改。
    - 保存并运行workflow。
    - 等待几分钟，网站应该已经部署成功。在之后的github提交会自动部署到网站。


---

**N.B.** 子模块git submodule的使用

查看子模块状态：
```bash
cat .gitmodules
git submodule
```
*查看子模块内容：*
```bash
git submodule update --init --recursive
cd path/to/submodule  # 进入子模块文件夹
git status            # 查看子模块的状态
```
*添加/更新子模块：*
```bash
git submodule add <repo_url> path/to/submodule  # 添加子模块
git submodule update --remote  # 更新子模块到最新提交
```
*删除子模块：*
```bash
git rm --cached path/to/submodule  # 删除子模块缓存
rm -rf .git/modules/path/to/submodule  # 删除子模块文件夹
```

---

