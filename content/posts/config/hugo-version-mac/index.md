---
title: "在 MacOS 中安装指定版本 Hugo"
date: 2024-10-24
draft: false
description: "省流：从github下载后拖到bin里"
tags: ["MacOS", "Hugo"]
---

## 问题

在本地搭建 Hugo 环境，运行 `hugo server` 时报 `WARN`：

```shell
WARN  Module "blowfish" is not compatible with this Hugo version: 0.87.0/0.135.0;
run "hugo mod graph" for more information.
```

但是 Homebrew 中只有最新版的 `hugo`

## 解决

1. 去 Hugo 的 [Github-Releases](https://github.com/gohugoio/hugo/releases) 页面找到需要的指定版本
2. 根据电脑系统定位到对应的压缩包进行下载
3. 解压，文件结构为
	```
	.
	├── LICENSE
	├── README.md
	└── hugo
	```
4. 将可执行文件 `hugo` 移动到 `/usr/local/bin`
   ```
   mv hugo /usr/local/bin
   ```

## 参考

[Hugo 安装指定版本 - SEVEN TUBE](https://hishark777.home.blog/2020/10/27/hugo-install-version/)