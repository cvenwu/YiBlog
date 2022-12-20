---
title: 为go项目编写Makefile
date: 2022-12-09 15:11:14
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
katex:
aplayer:
---

> 每次编写Go项目之后，都需要手动执行一系列命令编译成可执行文件，较为繁琐，在本文中我们推荐使用C/C++中盛行的Makefile来进行Go项目的编译等操作


{% note warning modern %}
{% label 注意事项 red %}：如果拷贝如下文件之后报错 Makefile missing separator. Stop. 请将前面的缩进替换为tab键缩进
{% endnote %}

用法：复制下面的代码，修改BINARY变量为自己的可执行程序名字即可


```makefile
# 定义编译出的可执行程序名
BINARY="main"
# 编译
build:
	CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build main.go -o ${BINARY}

.PHONY: all build run gotool clean help

clean:
	@if [ -f ${BINARY} ] ; then rm ${BINARY} ; fi

all: gotool build

run:
	@go run ./

gotool:
	go fmt ./
	go vet ./

help:
	@echo "make - 格式化 Go 代码, 并编译生成二进制文件"
	@echo "make build - 编译 Go 代码, 生成二进制文件"
	@echo "make run - 直接运行 Go 代码"
	@echo "make clean - 移除二进制文件和 vim swap files"
	@echo "make gotool - 运行 Go 工具 'fmt' and 'vet'"
```