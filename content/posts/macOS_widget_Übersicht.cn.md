---
author: "Suki Xuu"
title: "macOS 上的小组件桌面 --Übersicht"
date: "2025-02-19"
description: "使用Übersicht在macOS上创建小组件"
cntags: ["macOS", "Übersicht", "小组件"]
ShowToc: true
ShowBreadCrumbs: false
---

自定义 macOS 上的小组件，免费创建小组件桌面，使用开源工具[Übersicht](https://tracesof.net/uebersicht/#sponsor)

<!--more-->

## 1. 安装 Übersicht
- 下载安装包
	```bash
    brew install --cask ubersicht
	```
- 打开 `Übersicht.app` 初始化
双击打开 `Übersicht.app` 后，并不会有任何效果，因为我们还没有创建任何小组件。但会创建一个文件夹在 `~/Library/Application\ Support/Übersicht/widgets`，用于存放小组件的配置文件。

## 2. 创建小组件, 这里使用todo list 小组件作为示例。
*在[官网](https://tracesof.net/uebersicht/#sponsor)找喜欢的组件，直接使用, 官网有详细的组件介绍和使用方法。*
- 找到目标路径（下载后的文件所存放的路径）
	```bash
    cd ~/Library/Application\ Support/Übersicht/widgets
	```
- 下载组件文件
	```bash
    curl -O https://raw.githubusercontent.com/KalpShah999/Ubersicht-ToDo-Widget/master/todo.widget.zip  # 下载todo组件文件
    tar -zxvf todo.widget.zip  # 解压文件
    rm todo.widget.zip  # 删除压缩文件
  ```

- 在右上角的 `Übersicht` 图标上点击 `Refresh All Widgets`，刷新小组件。

