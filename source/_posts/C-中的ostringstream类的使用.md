
---
title: C++中的ostringstream类的使用
date: 2022-12-17 14:56:08
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

ostringstream是ostream的一个类，主要用于将数据写入string中。使用ostringstream的方法如下：
> 记得引入头文件：`#include <sstream>`
1. 创建ostringstream对象：`ostringstream oss;`
2. 向ostringstream对象中写入数据：`oss << "This is an example of writing data into an ostringstream object.";`
3. 从ostringstream对象中读取数据：`string str = oss.str();`


```c++
#include <iostream>
#include <sstream>

using namespace std;
int main(int argc, char const *argv[])
{
	ostringstream oss;
	oss << "this is namespace" << endl;
	cout << oss.str() << endl;
	return 0;
}
```