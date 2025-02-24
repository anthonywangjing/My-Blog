---
title: hexo 部署
tags:
  - 杂项
category: 杂项
---



## 介绍

Hexo 是一个快速、简单且功能强大的静态博客框架。它基于 Node.js 构建，使用 Markdown 文件生成静态网页，非常适合开发者和技术爱好者用来搭建博客和网站。Hexo 的设计目标是易于使用、快速生成，并且具有高度的可定制性

## 特点

- 速度： Hexo 是一个静态网站生成器，意味着所有的网页都会在生成时预先构建好，加载速度非常快。通过并行处理，Hexo 可以迅速生成数百个页面。
- 简单的配置和使用： Hexo 提供简洁的命令行接口，用户可以通过简单的命令来生成、部署和管理博客。
- Markdown 支持： 你可以使用 Markdown 编写文章，Hexo 会将它们转换为静态 HTML 文件。
- 多种主题和插件支持： Hexo 有丰富的社区支持，你可以选择大量的主题和插件来定制你的博客。主题控制着博客的外观，插件为博客添加额外功能（如评论、统计、SEO 优化等）。
- 跨平台支持： 由于 Hexo 是基于 Node.js 构建的，所以它支持跨平台（Windows、Linux、macOS），可以在各种操作系统上运行。
- 部署支持： Hexo 支持多种部署方式，包括 GitHub Pages、GitLab Pages、私有服务器、FTP 等。你可以通过配置文件来选择部署方式。

## hexo 配置

Hexo 的配置文件通常是 /_config.yml，用于设置网站的基本信息和行为。常见的配置项包括：

- 网站名称：设置博客的名称。
- 语言和时区：可以选择博客的语言和时区。
- 主题设置：设置主题以及主题相关的配置文件。
- 部署设置：设置如何将生成的静态文件上传到远程服务器

```
title: My Blog
subtitle: A personal blog
description: This is my blog where I share my thoughts.
author: Your Name
language: en
timezone: Asia/Shanghai
```

## hexo 常用命令

| 命令                  | 说明                             |
| --------------------- | -------------------------------- |
| hexo new post "Title" | 创建新文章，保存在source/_posts/ |
| hexo generate         | 生成静态文件，输出到 public/     |
| hexo server           | 启动本地服务器，预览博客         |
| hexo deploy           | 部署生成的博客到远程服务器       |
| hexo clean            | 清除缓存和生成的文件             |
| hexo list             | 查看所有文章和页面               |

## 部署

### 本地部署

#### 1.安装 Node.js和 git

访问 node官网，选择合适版本进行安装（推荐18版本的）
https://nodejs.org/en/download

2.安装完成后，可通过命令检查是否安装成功

```
node -v
npm -v
```

访问Git官网，根据官网提示安装

#### 2.安装Hexo

通过终端或命令行工具进行安装

```
npm install hexo-cli -g
```

#### 3.创建一个新的 Hexo 项目

在存放 Hexo博客的目录下，执行以下命令创建新的Hexo 项目

```
hexo init my-blog
```

my-blog 是项目目录名称

#### 4.安装依赖

项目创建完成后，进入项目目录并安装 Hexo所需的依赖：

```
cd my-blog
npm install
```

#### 5.生成静态文件

每次修改完内容后，可使用下列内容生成静态页面

```
hexo generate 
```

这会在项目目录下的 public/ 文件夹中生成静态文件

6.启动本地开发服务器

在Hexo 项目目录下，运行以下命令来启动本地开发服务器

```
hexo server
```

可通过 http://localhost:4000 上访问hexo博客内容

### 服务器部署（ubuntu）

#### 安装依赖

```
apt update
apt install nodejs npm 
node -v 
npm -v
```

#### 安装 Hexo

```
npm install -g hexo-cli
```

#### 初始化 Hexo 项目

```
mkdir hexo-blog
cd hexo-blog
hexo init
npm install
```

#### 安装并配置nginx反向代理

**安装nginx**

```
apt update
apt install nginx 
```

**配置nginx**
添加如下配置

```
server {
    listen 80;
    server_name yourdomain.com;
    
    root /var/www/my-blog/public;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

**重启nginx**

```
nginx -t
nginx -s reload
```

可通过 http://yourdomain.com 上访问hexo博客内容

### 部署到 GitHub Pages

GitHub Pages 是一个非常适合托管静态博客的免费服务。

#### 创建 GitHub 仓库

登录（GitHub），创建一个新的仓库，命名为 your-username.github.io（your-username 是Github 用户名）

#### 安装 Hexo 部署插件

Hexo 提供了一个部署插件，可将博客文件部署到 GitHub Pages 上

```
npm install hexo-deployer-git --save
```

#### 配置 _config.yml 文件

在 Hexo 项目的根目录下，找到 _config.yml 配置文件，配置 deploy 部分：

```
url: https://anthonywangjing.github.io   
root: /My-Blog/

deploy:
  type: 'git'
  repo: git@github.com:anthonywangjing/my-blog.git  //ssh连接
  branch: master      //部署的分支 
```

#### 部署 Hexo 博客

```
hexo clean    //清理缓存
hexo generate  //生成静态文件
hexo deploy    //远端部署
```

#### 验证部署

访问 https://your-username.github.io/{项目名}，便可访问 Hexo博客，如 https://anthonywangjing.github.io/My-Blog
