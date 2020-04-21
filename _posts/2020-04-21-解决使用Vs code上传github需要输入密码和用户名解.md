---
layout:     post
title:      解决使用VS Code上传Github每次都需要输入密码和用户名的问题
subtitle:
date:       2020-04-21
author:     BY 快乐小猪
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - VS Code
    - Github
---

# 解决使用VS Code上传Github每次都需要输入密码和用户名的问题

使用下面的命令可以解决
 git config --global credential.helper store

 命令行随后会提示输入用户名和密码，输入密码是不会有任何显示状态变化，输完直接回车就好。

再重启vscode，进行git操作，vscode就不再让我们输入用户名和密码啦！
