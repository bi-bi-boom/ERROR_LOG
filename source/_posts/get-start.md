---
title: Get Start
date: 2020-11-06 10:48:31
categories: blog
tags:
---

## Installation

请确保本机已安装 npm，[官方链接](https://www.npmjs.com/get-npm)

请确保已经 clone 这个 repo，[GitHub 链接](https://github.com/bi-bi-boom/ERROR_LOG)

请确保本机已安装 hexo，[官方链接](https://hexo.io/zh-cn/)

在根目录下运行

```shell
npm install
```

<!-- More -->

## 写作

hexo 的规则参考 [官网 doc](https://hexo.io/zh-cn/docs/writing)

发布时，运行

```shell
hexo g
```

来生成 public/ 目录；

运行

```shell
hexo d
```

上传到 GitHub。

> 关于文字排版参考 [这篇文章](https://github.com/xitu/gold-miner/wiki/%E8%AF%91%E6%96%87%E6%8E%92%E7%89%88%E8%A7%84%E5%88%99%E6%8C%87%E5%8C%97)

## github 发布时权限问题

- hexo 发布 （deploy）之前需要先 在 git 里获得添加ssh
- 按下 Win 键寻找并且运行 Git Bash。没有的话百度或者 Google 下载一下，搜索 “git 下载”。
- 那一步 hexo d 如果最后没有成功，很可能是没有 git 权限。
  - 解决办法：配置关于自己 github 的 ssh。
  - .
  - .
  - .
  - .
  - .
  - .
- ssh 配置完成后重新 hexo d，就可以把本地的生成的内容发布到远端。

## 隔一段时间之后

- 本地的ssh很可能需要再次添加到本地客户端（不需要 github 再去生成 ssh 秘钥）下面是解决办法
  - 两句话：
  - >eval $(ssh-agent -s)
  - >ssh-add ~/.ssh/zzxssh

- 其中这个 zzxssh是我命名的 ssh 许可文件

- 可以使用 ls -al ~/.ssh  先查看 ssh 文件有哪些

| 指令 | 作用 |
| :---:| :---:|
|hexo g|本地生成静态html|
|hexo d|本地工程发布到远端|
  