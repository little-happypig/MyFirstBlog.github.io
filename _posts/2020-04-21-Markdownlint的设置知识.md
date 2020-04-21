---
layout:     post
title:      Markdownlint的设置知识
subtitle:
date:       2020-04-21 10:06:00
author:     BY 快乐小猪
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - VS Code
    - Github
---

# Markdownlint的设置知识

VS Code的插件Markdownlint经常会提示一些你觉得不用修改的错误问题，比如每个文档不该有多个最高级标签（MD025）,这时候打开插件栏，右键点Markdownlint,选设置菜单，然后点击在Setting.json中编辑

* 修改示例，例如你要关闭“MD025”和“MD040”提示，作如下修改：

```
{
    "editor.suggestSelection": "first",
    "vsintellicode.modify.editor.suggestSelection": "automaticallyOverrodeDefaultValue",
    "git.autofetch": true,
    "markdownlint.config": {

            "MD025": false,  
            "MD040": false
    },
    "git.enableSmartCommit": true
}
```

多个项目用逗号分隔开。
