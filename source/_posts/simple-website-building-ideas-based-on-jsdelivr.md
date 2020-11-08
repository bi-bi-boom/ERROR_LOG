---
title: 基于 jsDelivr 的简单建站思路
date: 2020-07-26
updated: 2020-11-08 01:33:10
categories: Web
tags:
  - "author: cloxnu"
  - JavaScript
---

暑假期间，心血来潮想要写一个自己的 travel blog，想要用最低成本的方式写一个最稳定的 blog 网站，以下是我制作这个网站的总体思路，仅供参考。

#### 我使用的服务

- 服务器提供商使用 [Linode](https://www.linode.com)，位于美国加州。
- 使用 [Cloudflare](https://www.cloudflare.com) 作为全球 cdn 加速。
- 将全站备份于 GitHub，并使用 [jsDelivr](https://www.jsdelivr.com) 加速 GitHub 上的静态资源。

<!-- More -->

这个网站是 [an.dog](https://an.dog)，以下是 logo 和截图。

{% asset_img travelDogIconHome.svg %}

{% asset_img travelDogHome.png %}

## 整体思路

jsDelivr 的作用主要用来加速需网络速度较快的静态资源，如图片、视频等等。由于 jsDelivr 在国内有服务器，所以国内的访问速度很快，jsDelivr 的使用参考 [官网](https://www.jsdelivr.com)，简单来说就是通过请求 URL `https://cdn.jsdelivr.net/gh/[用户名]/[仓库名]/[文件路径]` 来访问 GitHub 里的文件，由于有时候 GitHub 的修改可能导致 jsDelivr 没有及时更新，建议在 GitHub 用 release 的方式进行 cdn 加速，这种方法需要访问 `https://cdn.jsdelivr.net/gh/[用户名]/[仓库名]@[版本名]/[文件路径]` 来使用 cdn。[an.dog 的 GitHub 链接](https://github.com/CLOXnu/travelblog)

整站的文章写在根目录的 `content/` 目录下，每篇文章带有一个 `info.json`，用来列举文章的详细信息。后端语言使用 PHP，动态读取 `content/` 目录下的文件，然后前端 JavaScript 将 Markdown 转为 Html。

这里使用一个 JavaScript 工具 [Marked](https://marked.js.org/) 完成 Markdown 转 Html 的工作。在 Marked 的说明文档中介绍到，可以使用 renderer 将 Markdown 转换过程中遇到指定的内容并转换成需要的格式，这样就可以将文章中引用到的图片转换成 jsDelivr 的地址了（如下图）（那个 baseURL 就是 jsDelivr cdn 的前缀：`https://cdn.jsdelivr.net/gh/...`）

{% asset_img marked.png %}

> 图片中那个 `level === 2 || level === 4` 的意思是我将标题等级为 2 和 4 的标题加一个 id，后面可以定位这些标题。
