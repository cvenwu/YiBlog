---
title: 性能测试工具ab安装与使用
date: 2022-12-17 14:31:02
password: test
message: 文章尚未撰写完成，完成后会解密
tags:
updated:
categories:
keywords:
description:
top_img:
comments:
cover:
toc:
toc_number:
toc_style_simple:
copyright:
copyright_author:
copyright_author_href:
copyright_url:
copyright_info:
mathjax:
katex:
aplayer:
highlight_shrink:
aside:
---

## 背景
日常开发过程中，在我们开发接近尾声总要在开发环境或者测试环境进行各种测试，其中最重要的便是性能测试，一个系统的成败不仅仅需要运行稳定、结果正确、占用资源尽可能小，还要在基础上达到极致的性能。作为开发人员，我们需要对常见的性能测试工具如ab等需要掌握基本的原理以及熟练的使用


这里最好画一个图，描述一下常用开发流程中的图

## 安装

1. 执行`yum install httpd-tools`进行安装
2. 