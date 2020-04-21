---
layout:     post
title:      Markdownlint规则详细介绍及自定义参数设置
subtitle:   
date:       2020-04-21
author:     BY
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - Markdown
    - Rules
    - 参数
    - 设置
---

## Markdownlint规则详细介绍及自定义参数设置

markdownlint是vscode上一款非常好用的 Markdown 格式检查扩展工具，它规定了许多规则并实时对文档进行检查，防止一些语法错误，同时维持文档风格的统一，使用此工具有助于形成一个良好的写作习惯和规范。但因其规则较多，写文档时很容易就出错（或不符合规则），所以需要对工具的规则有一个详细的了解，另外，有时工作要求的文档风格与markdownlint工具规定的规则并不相同，比如标题、列表的创建格式，缩进的空格数等等，这时就需要对规则进行一定的设置。

本文主要参考markdownlint的rules文档，对每一个规则都进行了说明，指明了一些规则中可以设置的参数，便于用户设置相应的规则。

* MD001 - Heading levels should only increment by one level at a time
标题级数每次只能扩大1, 也就是不能隔级创建标题（从1级到6级的顺序）

MD002 - First heading should be a top level heading
文档的第一个标题必须是最高级的标题（标题等级1级到6级逐渐降低）

参数：
"level"：指定最高级标题的级数，默认是1

* MD003 - Heading style
整篇文档要采用一致的标题格式

参数：
"style"：字符串，指定文档标题的格式，有("consistent", "atx", "atx_closed", "setext", "setext_with_atx", "setext_with_atx_closed")五种，默认是"consistent"，也就是整篇文档一致

标题格式必须统一，一般不能混用，但"setext_with_atx", "setext_with_atx_closed"格式可以在"setext"格式二级标题后接着使用"atx"或"atx_closed"格式的标题

* MD004 - Unordered list style
整篇文档定义无序列表的格式要一致

参数：
"style"：字符串，指定无序列表的定义格式，有("consistent", "asterisk", "plus", "dash", "sublist")五种，分别表示“定义时符号前后一致”，“用星号定义”，“用加号定义”，“用减号定义”，“定义多重列表时用不同的符号定义”，默认是"consistent"

* MD005 - Inconsistent indentation for list items at the same level
同一级的列表缩进必须一致
在有序列表中，前面的数字序号可以左对齐，也可以右对齐

* MD006 - Consider starting bulleted lists at the beginning of the line
1级列表不能缩进

* MD007 - Unordered list indentation
无序列表嵌套缩进时默认采用两个空格

参数：
"ident"：指定无序列表嵌套时缩进的空格数，默认是2

* MD009 - Trailing spaces
行尾最多可以添加两个空格，超过会给出警告，两个空格正好可以用于换行

参数：
"br_spaces"：指定在行尾可以添加的空格数目，空格数目建议大于等于2，如果小于2，会默认为0，也就是不允许任何行尾的空格
"list_item_empty_lines"：字符串，指定在列表中是否(true or false)用默认的空格数缩进空行，有的解释器会要求列表中的空行要缩进

* MD010 - Hard tabs
不能使用tab键缩进，要使用空格

参数：
"code_blocks"：指定本条规则在代码块里是否(true or false)生效

* MD011 - Reversed link syntax
检查内联形式的链接的创建方式是否错误，中括号和圆括号是否用对

* MD012 - Multiple consecutive blank lines
文档中不能有连续的空行，在代码块中此规则不会生效

参数：
"maximum"：指定文档中可以连续的最多空行数，默认值是1

* MD013 - Line length
默认行的最大长度是80，此规则对代码块、表格、标题也生效

参数：
"line_length"：指定行的最大长度，默认是80
"heading_line_length"：指定标题行的最大长度，默认是80
"code_blocks"：指定规则是否(true or false)对代码块生效，默认true
"tables"：指定规则是否(true or false)对表格生效，默认true
"hesdings"：指定规则是否(true or false)对标题生效，默认true

* MD014 - Dollar signs used before commands without showing output
在代码块中，终端命令前不需要有美元符号($)
如果代码块中既有终端命令，也有命令的输出，则终端命令前可以有美元符号($)，如：

$ ls
foo bar
$ cat foo
hello world

* MD018 - No space after hash on atx style heading
在"atx"格式的标题中，#号和文字间需用一个空格隔开

* MD019 - Multiple spaces after hash on atx style heading
在"atx"格式的标题中，#号和文字间只能用一个空格隔开，不能有多余的空格

* MD020 - No space inside hashes on closed atx style heading
在"closed_atx"格式的标题中，文字和前后的#号之间需用一个空格隔开

* MD021 - Multiple spaces inside hashes on closed atx style heading
在"closed_atx"格式的标题中，文字和前后的#号之间只能用一个空格隔开，不能有多余的空格

* MD022 - Headings should be surrounded by blank lines
标题行的上下行必须都是空行

参数：
"lines_above"：指定标题行上方的空行数，默认为1，可以设为更大或0
"lines_below"：指定标题行下方的空行数，默认为1，可以设为更大或0

注意当此处的空行设为比1大的数时，规则MD012的设置也要改

* MD023 - Headings must start at the beginning of the line
标题行不能缩进

* MD024 - Multiple headings with the same content
文档不能有内容重复的标题

参数：
"siblings_only"：默认为false，设为true时，不同标题下的子标题内容可以重复

* MD025 - Multiple top level headings in the same document
同一文档只能有一个最高级的标题，默认是只能有一个1级标题

参数：
"level"：指定文档最高级的标题，默认是1
"front_matter_title"：字符串，指定在文档开头处的front matter中的标题，这个标题将作为整篇文档的最高级标题，如果文档中再次出现最高级标题，将会给出警告，另外，如果不想在front matter中指定标题，就把本参数的值设置为""

* MD026 - Trailing punctuation in heading
标题行末尾不能有以下标点符号：".,;:!?"

参数：
"punctuation"：字符串，指定标题行尾不能有的标点符号，默认是".,;:!?"

此规则默认的是英文的标点符号，中文标点符号不在规则之内

* MD027 - Multiple spaces after blockquote symbol
创建引用区块时，右尖括号 ( > ) 和文字之间有且只能有一个空格

* MD028 - Blank line inside blockquote
两个引用区块间不能仅用一个空行隔开或者同一引用区块中不能有空行，如果一行中没有内容，则这一行要用>开头

* MD029 - Ordered list item prefix
有序列表的前缀序号格式必须只用1或者从1开始的加1递增数字("one_or_ordered")

参数：
"style"：字符串，指定前缀序号的格式，("one","ordered","one_or_ordered","zero")，分别表示只用1做前缀，用从1开始的加1递增数字做前缀，只用1或者从1开始的加1递增数字做前缀，只用0做前缀，默认值是"one_or_ordered"

本条规则支持在前缀序号中补0，以实现对齐，如：

...
08.  one
09.  two
10.  three
...

* MD030 - Spaces after list markers
列表（有序、无序）的前缀符号和文字之间用1个空格隔开
在列表嵌套或者同一列表项中有多个段落时，无序列表缩进两个空格，有序列表缩进3个空格

参数：
"ul_single","ol_single","ul_multi","ol_multi"：分别规定无序列表单个段落，有序列表单个段落，无序列表多个段落，有序列表多个段落的前缀符号和文字之间的空格数，默认是1

* MD031 - Fenced code blocks should be surrounded by blank lines
单独的代码块前后需要用空行隔开（除非是在文档开头或末尾），否则有些解释器不会解释为代码块

* MD032 - Lists should be surrounded by blank lines
列表（有序、无序）前后需要用空行隔开，否则有些解释器不会解释为列表
列表的缩进必须一致，否则会警告

* MD033 - Inline HTML
文档中不允许使用HTML语句

参数：
"allowed_elements"：自定义允许的元素，是一个字符串数组，默认是空(empty)

* MD034 - Bare URL used
单纯的链接地址需要用尖括号 (<>) 包裹，否则有些解释器不会解释为链接

* MD035 - Horizontal rule style
创建水平线时整篇文档要统一(consistent)，要和文档中第一次创建水平线使用的符号一致

参数：
"style"：字符串，指定创建水平线的方式，值有：("consistent","***","---","___")，默认是"consistent"

* MD036 - Emphasis used instead of a heading
不能用强调代替标题

参数：
"punctuation"：字符串，指定用于结尾的标点符号，以此符号结尾的强调不会被视为以强调代替标题，默认值是".,;:!?"

此规则会检查只包含强调的单行段落，如果这种段落不是以指定的标点符号结尾，则会被视为以强调代替标题，会给出警告

* MD037 - Spaces inside emphasis markers
用于创建强调的符号和强调的的文字之间不能有空格

* MD038 - Spaces inside code span elements
当用单反引号创建代码段的时候，单反引号和它们之间的代码不能有空格
如果要把单反引号嵌入到代码段的首尾，创建代码段的单反引号和嵌入的单反引号间要有一个空格隔开

* MD039 - Spaces inside link text
链接名和包围它的中括号之间不能有空格，但链接名中间可以有空格，如：

[百 度](http://www.baidu.com "百 度")

* MD040 - Fenced code blocks should have a language specified
单独的代码块（此处是指上下用三个反引号包围的代码块）应该指定代码块的编程语言，这一点有助于解释器对代码进行代码高亮

* MD041 - First line in file should be a top level heading
文档的第一个非空行应该是文档最高级的标题，默认是1级标题

参数：
"level"：指定文档最高级的标题，默认是1
"front_matter_title"：字符串，指定在文档开头处的front matter中的标题，这个标题将作为整篇文档的最高级标题，另外，如果不想在front matter中指定标题，就把本参数的值设置为""

* MD042 - No empty links
链接的地址不能为空

* MD043 - Required heading structure
要求标题遵循一定的结构，默认是没有规定的结构("null")

参数：
"headings"：字符串数组，指定标题需要遵循的结构，默认是"null"，可以自行指定结构，如；

[
    "# head",
    "## item",
    "### detail",
    "*"
]
星号(*)表示对应的标题是可选的，没有强制要求，本条具体可以参照MD043

* MD044 - Proper names should have the correct capitalization
指定一些名称，会检查它是否有正确的大写

参数：
"names"：字符串数组，指定要检查需要大写的名称，默认是空("null")
"code_blocks"：指定本规则是否(true or false)对代码块生效，默认是true
一些经常使用的名称可以使用本规则防止其拼写错误，比如JavaScript中字母J和S需要大写，就可以写到参数"names"中，防止写错

* MD045 - Images should have alternate text (alt text)
图片链接必须包含描述文本（alt text）

* MD046 - Code block style
整篇文档采用一致的代码格式

参数：
"style": 字符串，指定代码块定义格式，有（"consistent","fenced","indented"）三种，分别代表：文档上下文一致，使用三个反引号隔开，使用缩进，默认是上下文一致

* MD047 - Files should end with a single newline character
文档需用一个空行结尾


# Rules

This document contains a description of all rules, what they are checking for, as well as an examples of documents that break the rule and corrected versions of the examples. Any rule whose heading is ~~struck through~~ is deprecated, but still provided for backward-compatibility.



## MD001 - Heading levels should only increment by one level at a time

Tags: headings, headers

Aliases: heading-increment, header-increment

This rule is triggered when you skip heading levels in a markdown document, for example:

```
# Heading 1

### Heading 3

We skipped out a 2nd level heading in this document
```

When using multiple heading levels, nested headings should increase by only one level at a time:

```
# Heading 1

## Heading 2

### Heading 3

#### Heading 4

## Another Heading 2

### Another Heading 3
```

Rationale: Headings represent the structure of a document and can be confusing when skipped - especially for accessibility scenarios. More information: https://www.w3.org/WAI/tutorials/page-structure/headings/.



## ~~MD002 - First heading should be a top level heading~~

Tags: headings, headers

Aliases: first-heading-h1, first-header-h1

Parameters: level (number; default 1)

> Note: *MD002 has been deprecated and is disabled by default.* [MD041/first-line-heading](https://github.com/DavidAnson/markdownlint/blob/master/doc/Rules.md#md041) offers an improved implementation.

This rule is intended to ensure document headings start at the top level and is triggered when the first heading in the document isn't an h1 heading:

```
## This isn't an H1 heading

### Another heading
```

The first heading in the document should be an h1 heading:

```
# Start with an H1 heading

## Then use an H2 for subsections
```

Note: The `level` parameter can be used to change the top level (ex: to h2) in cases where an h1 is added externally.

Rationale: The top level heading often acts as the title of a document. More information: <https://cirosantilli.com/markdown-style-guide#top-level-header.>

## MD003 - Heading style

Tags: headings, headers

Aliases: heading-style, header-style

Parameters: style ("consistent", "atx", "atx_closed", "setext", "setext_with_atx", "setext_with_atx_closed"; default "consistent")

This rule is triggered when different heading styles (atx, setext, and 'closed' atx) are used in the same document:

```
# ATX style H1

## Closed ATX style H2 ##

Setext style H1
===============
```

Be consistent with the style of heading used in a document:

```
# ATX style H1

## ATX style H2
```

The setext_with_atx and setext_with_atx_closed doc styles allow atx-style headings of level 3 or more in documents with setext style headings:

```
Setext style H1
===============

Setext style H2
---------------

### ATX style H3
```

Note: the configured heading style can be a specific style to use (atx, atx_closed, setext, setext_with_atx, setext_with_atx_closed), or simply require that the usage be consistent within the document.

Rationale: Consistent formatting makes it easier to understand a document.

## MD004 - Unordered list style

Tags: bullet, ul

Aliases: ul-style

Parameters: style ("consistent", "asterisk", "plus", "dash", "sublist"; default "consistent")

This rule is triggered when the symbols used in the document for unordered list items do not match the configured unordered list style:

```
* Item 1
+ Item 2
- Item 3
```

To fix this issue, use the configured style for list items throughout the document:

```
* Item 1
* Item 2
* Item 3
```

The configured list style can be a specific symbol to use (asterisk, plus, dash), can require that usage be consistent within the document, or can require that each sublist have a consistent symbol that is different from its parent list.

For example, the following is valid for the `sublist` style because the outer-most indent uses asterisk, the middle indent uses plus, and the inner-most indent uses dash:

```
* Item 1
  + Item 2
    - Item 3
  + Item 4
* Item 4
  + Item 5
```

Rationale: Consistent formatting makes it easier to understand a document.

## MD005 - Inconsistent indentation for list items at the same level

Tags: bullet, ul, indentation

Aliases: list-indent

This rule is triggered when list items are parsed as being at the same level, but don't have the same indentation:

```
* Item 1
  * Nested Item 1
  * Nested Item 2
   * A misaligned item
```

Usually this rule will be triggered because of a typo. Correct the indentation for the list to fix it:

```
* Item 1
  * Nested Item 1
  * Nested Item 2
  * Nested Item 3
```

Sequentially-ordered list markers are usually left-aligned such that all items have the same starting column:

```
...
8. Item
9. Item
10. Item
11. Item
...
```

This rule also supports right-alignment of list markers such that all items have the same ending column:

```
...
 8. Item
 9. Item
10. Item
11. Item
...
```

Rationale: Violations of this rule can lead to improperly rendered content.



## ~~MD006 - Consider starting bulleted lists at the beginning of the line~~

Tags: bullet, ul, indentation

Aliases: ul-start-left

This rule is triggered when top level lists don't start at the beginning of a line:

```
Some text

  * List item
  * List item
```

To fix, ensure that top level list items are not indented:

```
Some test

* List item
* List item
```

Note: This rule is triggered for the following scenario because the unordered sublist is not recognized as such by the parser. Not being nested 3 characters as required by the outer ordered list, it creates a top-level unordered list instead.

```
1. List item
  - List item
  - List item
1. List item
```

Rationale: Starting lists at the beginning of the line means that nested list items can all be indented by the same amount when an editor's indent function or the tab key is used to indent. Starting a list 1 space in means that the indent of the first nested list is less than the indent of the second level (3 characters if you use 4 space tabs, or 1 character if you use 2 space tabs).



## MD007 - Unordered list indentation

Tags: bullet, ul, indentation

Aliases: ul-indent

Parameters: indent, start_indented (number; default 2, boolean; default false)

This rule is triggered when list items are not indented by the configured number of spaces (default: 2).

Example:

```
* List item
   * Nested list item indented by 3 spaces
```

Corrected Example:

```
* List item
  * Nested list item indented by 2 spaces
```

Note: This rule applies to a sublist only if its parent lists are all also unordered (otherwise, extra indentation of ordered lists interferes with the rule).

The `start_indented` parameter allows the first level of lists to be indented by the configured number of spaces rather than starting at zero (the inverse of MD006).

Rationale: Indenting by 2 spaces allows the content of a nested list to be in line with the start of the content of the parent list when a single space is used after the list marker. Indenting by 4 spaces is consistent with code blocks and simpler for editors to implement. Additionally, this can be a compatibility issue for multi-markdown parsers, which require a 4-space indents. More information: <https://cirosantilli.com/markdown-style-guide#indentation-of-content-inside-lists> and <http://support.markedapp.com/discussions/problems/21-sub-lists-not-indenting.>

## MD009 - Trailing spaces

Tags: whitespace

Aliases: no-trailing-spaces

Parameters: br_spaces, list_item_empty_lines, strict (number; default 2, boolean; default false, boolean; default false)

This rule is triggered on any lines that end with unexpected whitespace. To fix this, remove the trailing space from the end of the line.

The `br_spaces` parameter allows an exception to this rule for a specific number of trailing spaces, typically used to insert an explicit line break. The default value allows 2 spaces to indicate a hard break (<br> element).

Note: You must set `br_spaces` to a value >= 2 for this parameter to take effect. Setting `br_spaces` to 1 behaves the same as 0, disallowing any trailing spaces.

By default, this rule will not trigger when the allowed number of spaces is used, even when it doesn't create a hard break (for example, at the end of a paragraph). To report such instances as well, set the `strict` parameter to `true`.

```
Text text text
text[2 spaces]
```

Using spaces to indent blank lines inside a list item is usually not necessary, but some parsers require it. Set the `list_item_empty_lines` parameter to `true` to allow this (even when `strict` is `true`):

```
- list item text
  [2 spaces]
  list item text
```

Rationale: Except when being used to create a line break, trailing whitespace has no purpose and does not affect the rendering of content.



## MD010 - Hard tabs

Tags: whitespace, hard_tab

Aliases: no-hard-tabs

Parameters: code_blocks (boolean; default true)

This rule is triggered by any lines that contain hard tab characters instead of using spaces for indentation. To fix this, replace any hard tab characters with spaces instead.

Example:

```
Some text

	* hard tab character used to indent the list item
```

Corrected example:

```
Some text

    * Spaces used to indent the list item instead
```

You have the option to exclude this rule for code blocks. To do so, set the `code_blocks` parameter to `false`. Code blocks are included by default since handling of tabs by tools is often inconsistent (ex: using 4 vs. 8 spaces).

Rationale: Hard tabs are often rendered inconsistently by different editors and can be harder to work with than spaces.



## MD011 - Reversed link syntax

Tags: links

Aliases: no-reversed-links

This rule is triggered when text that appears to be a link is encountered, but where the syntax appears to have been reversed (the `[]` and `()` are reversed):

```
(Incorrect link syntax)[https://www.example.com/]
```

To fix this, swap the `[]` and `()` around:

```
[Correct link syntax](https://www.example.com/)
```

Note: [Markdown Extra](https://en.wikipedia.org/wiki/Markdown_Extra)-style footnotes do not trigger this rule:

```
For (example)[^1]
```

Rationale: Reversed links are not rendered as usable links.



## MD012 - Multiple consecutive blank lines

Tags: whitespace, blank_lines

Aliases: no-multiple-blanks

Parameters: maximum (number; default 1)

This rule is triggered when there are multiple consecutive blank lines in the document:

```
Some text here


Some more text here
```

To fix this, delete the offending lines:

```
Some text here

Some more text here
```

Note: this rule will not be triggered if there are multiple consecutive blank lines inside code blocks.

Note: The `maximum` parameter can be used to configure the maximum number of consecutive blank lines.

Rationale: Except in a code block, blank lines serve no purpose and do not affect the rendering of content.



## MD013 - Line length

Tags: line_length

Aliases: line-length

Parameters: line_length, heading_line_length, code_block_line_length, code_blocks, tables, headings, headers, strict, stern (number; default 80 for *_length, boolean; default true (except strict/stern which default false))

> If `headings` is not provided, `headers` (deprecated) will be used.

This rule is triggered when there are lines that are longer than the configured `line_length` (default: 80 characters). To fix this, split the line up into multiple lines. To set a different maximum length for headings, use `heading_line_length`. To set a different maximum length for code blocks, use `code_block_line_length`

This rule has an exception when there is no whitespace beyond the configured line length. This allows you to still include items such as long URLs without being forced to break them in the middle. To disable this exception, set the `strict` parameter to `true` to report an issue when any line is too long. To warn for lines that are too long and could be fixed but allow lines without spaces, set the `stern` parameter to `true`.

For example (assuming normal behavior):

```
IF THIS LINE IS THE MAXIMUM LENGTH
This line is okay because there are-no-spaces-beyond-that-length
And this line is a violation because there are
This-line-is-also-okay-because-there-are-no-spaces
```

In `strict` or `stern` modes, the two middle lines above are a violation. The third line is a violation in `strict` mode, but allowed in `stern` mode.

You have the option to exclude this rule for code blocks, tables, or headings. To do so, set the `code_blocks`, `tables`, or `headings` parameter(s) to false.

Code blocks are included in this rule by default since it is often a requirement for document readability, and tentatively compatible with code rules. Still, some languages do not lend themselves to short lines.

Rationale: Extremely long lines can be difficult to work with in some editors. More information: https://cirosantilli.com/markdown-style-guide#line-wrapping.



## MD014 - Dollar signs used before commands without showing output

Tags: code

Aliases: commands-show-output

This rule is triggered when there are code blocks showing shell commands to be typed, and *all* of the shell commands are preceded by dollar signs ($):

```
$ ls
$ cat foo
$ less bar
```

The dollar signs are unnecessary in this situation, and should not be included:

```
ls
cat foo
less bar
```

Showing output for commands preceded by dollar signs does not trigger this rule:

```
$ ls
foo bar
$ cat foo
Hello world
$ cat bar
baz
```

Because some commands do not produce output, it is not a violation if *some* commands do not have output:

```
$ mkdir test
mkdir: created directory 'test'
$ ls test
```

Rationale: It is easier to copy/paste and less noisy if the dollar signs are omitted when they are not needed. See https://cirosantilli.com/markdown-style-guide#dollar-signs-in-shell-code for more information.



## MD018 - No space after hash on atx style heading

Tags: headings, headers, atx, spaces

Aliases: no-missing-space-atx

This rule is triggered when spaces are missing after the hash characters in an atx style heading:

```
#Heading 1

##Heading 2
```

To fix this, separate the heading text from the hash character by a single space:

```
# Heading 1

## Heading 2
```

Rationale: Violations of this rule can lead to improperly rendered content.



## MD019 - Multiple spaces after hash on atx style heading

Tags: headings, headers, atx, spaces

Aliases: no-multiple-space-atx

This rule is triggered when more than one space is used to separate the heading text from the hash characters in an atx style heading:

```
#  Heading 1

##  Heading 2
```

To fix this, separate the heading text from the hash character by a single space:

```
# Heading 1

## Heading 2
```

Rationale: Extra space has no purpose and does not affect the rendering of content.



## MD020 - No space inside hashes on closed atx style heading

Tags: headings, headers, atx_closed, spaces

Aliases: no-missing-space-closed-atx

This rule is triggered when spaces are missing inside the hash characters in a closed atx style heading:

```
#Heading 1#

##Heading 2##
```

To fix this, separate the heading text from the hash character by a single space:

```
# Heading 1 #

## Heading 2 ##
```

Note: this rule will fire if either side of the heading is missing spaces.

Rationale: Violations of this rule can lead to improperly rendered content.



## MD021 - Multiple spaces inside hashes on closed atx style heading

Tags: headings, headers, atx_closed, spaces

Aliases: no-multiple-space-closed-atx

This rule is triggered when more than one space is used to separate the heading text from the hash characters in a closed atx style heading:

```
#  Heading 1  #

##  Heading 2  ##
```

To fix this, separate the heading text from the hash character by a single space:

```
# Heading 1 #

## Heading 2 ##
```

Note: this rule will fire if either side of the heading contains multiple spaces.

Rationale: Extra space has no purpose and does not affect the rendering of content.



## MD022 - Headings should be surrounded by blank lines

Tags: headings, headers, blank_lines

Aliases: blanks-around-headings, blanks-around-headers

Parameters: lines_above, lines_below (number; default 1)

This rule is triggered when headings (any style) are either not preceded or not followed by at least one blank line:

```
# Heading 1
Some text

Some more text
## Heading 2
```

To fix this, ensure that all headings have a blank line both before and after (except where the heading is at the beginning or end of the document):

```
# Heading 1

Some text

Some more text

## Heading 2
```

The `lines_above` and `lines_below` parameters can be used to specify a different number of blank lines (including 0) above or below each heading.

Note: If `lines_above` or `lines_below` are configured to require more than one blank line, [MD012/no-multiple-blanks](https://github.com/DavidAnson/markdownlint/blob/master/doc/Rules.md#md012) should also be customized.

Rationale: Aside from aesthetic reasons, some parsers, including kramdown, will not parse headings that don't have a blank line before, and will parse them as regular text.



## MD023 - Headings must start at the beginning of the line

Tags: headings, headers, spaces

Aliases: heading-start-left, header-start-left

This rule is triggered when a heading is indented by one or more spaces:

```
Some text

  # Indented heading
```

To fix this, ensure that all headings start at the beginning of the line:

```
Some text

# Heading
```

Rationale: Headings that don't start at the beginning of the line will not be parsed as headings, and will instead appear as regular text.



## MD024 - Multiple headings with the same content

Tags: headings, headers

Aliases: no-duplicate-heading, no-duplicate-header

Parameters: siblings_only, allow_different_nesting (boolean; default `false`)

This rule is triggered if there are multiple headings in the document that have the same text:

```
# Some text

## Some text
```

To fix this, ensure that the content of each heading is different:

```
# Some text

## Some more text
```

If the parameter `siblings_only` (alternatively `allow_different_nesting`) is set to `true`, heading duplication is allowed for non-sibling headings (common in change logs):

```
# Change log

## 1.0.0

### Features

## 2.0.0

### Features
```

Rationale: Some markdown parsers generate anchors for headings based on the heading name; headings with the same content can cause problems with that.



## MD025 - Multiple top level headings in the same document

Tags: headings, headers

Aliases: single-title, single-h1

Parameters: level, front_matter_title (number; default 1, string; default "^\s*title:")

This rule is triggered when a top level heading is in use (the first line of the file is an h1 heading), and more than one h1 heading is in use in the document:

```
# Top level heading

# Another top level heading
```

To fix, structure your document so that there is a single h1 heading that is the title for the document, and all later headings are h2 or lower level headings:

```
# Title

## Heading

## Another heading
```

Note: The `level` parameter can be used to change the top level (ex: to h2) in cases where an h1 is added externally.

If [YAML](https://en.wikipedia.org/wiki/YAML) front matter is present and contains a `title` property (commonly used with blog posts), this rule treats that as a top level heading and will report a violation for any subsequent top level headings. To use a different property name in front matter, specify the text of a regular expression via the `front_matter_title` parameter. To disable the use of front matter by this rule, specify `""` for `front_matter_title`.

Rationale: A top level heading is an h1 on the first line of the file, and serves as the title for the document. If this convention is in use, then there can not be more than one title for the document, and the entire document should be contained within this heading.



## MD026 - Trailing punctuation in heading

Tags: headings, headers

Aliases: no-trailing-punctuation

Parameters: punctuation (string; default ".,;:!?。，；：！？")

This rule is triggered on any heading that has one of the specified normal or full-width punctuation characters as the last character in the line:

```
# This is a heading.
```

To fix this, remove the trailing punctuation:

```
# This is a heading
```

Note: The `punctuation` parameter can be used to specify what characters count as punctuation at the end of a heading. For example, you can change it to `".,;:!"` to allow headings that end with a question mark, such as in an FAQ. Setting the `punctuation` parameter to `""` allows all characters - and is equivalent to disabling the rule.

Rationale: Headings are not meant to be full sentences. More information: https://cirosantilli.com/markdown-style-guide#punctuation-at-the-end-of-headers



## MD027 - Multiple spaces after blockquote symbol

Tags: blockquote, whitespace, indentation

Aliases: no-multiple-space-blockquote

This rule is triggered when blockquotes have more than one space after the blockquote (`>`) symbol:

```
>  This is a block quote with bad indentation
>  there should only be one.
```

To fix, remove any extraneous space:

```
> This is a blockquote with correct
> indentation.
```

Rationale: Consistent formatting makes it easier to understand a document.



## MD028 - Blank line inside blockquote

Tags: blockquote, whitespace

Aliases: no-blanks-blockquote

This rule is triggered when two blockquote blocks are separated by nothing except for a blank line:

```
> This is a blockquote
> which is immediately followed by

> this blockquote. Unfortunately
> In some parsers, these are treated as the same blockquote.
```

To fix this, ensure that any blockquotes that are right next to each other have some text in between:

```
> This is a blockquote.

And Jimmy also said:

> This too is a blockquote.
```

Alternatively, if they are supposed to be the same quote, then add the blockquote symbol at the beginning of the blank line:

```
> This is a blockquote.
>
> This is the same blockquote.
```

Rationale: Some markdown parsers will treat two blockquotes separated by one or more blank lines as the same blockquote, while others will treat them as separate blockquotes.



## MD029 - Ordered list item prefix

Tags: ol

Aliases: ol-prefix

Parameters: style ("one", "ordered", "one_or_ordered", "zero"; default "one_or_ordered")

This rule is triggered for ordered lists that do not either start with '1.' or do not have a prefix that increases in numerical order (depending on the configured style). The less-common patterns of using '0.' as a first prefix or for all prefixes is also supported.

Example valid list if the style is configured as 'one':

```
1. Do this.
1. Do that.
1. Done.
```

Examples of valid lists if the style is configured as 'ordered':

```
1. Do this.
2. Do that.
3. Done.
0. Do this.
1. Do that.
2. Done.
```

All three examples are valid when the style is configured as 'one_or_ordered'.

Example valid list if the style is configured as 'zero':

```
0. Do this.
0. Do that.
0. Done.
```

Example invalid list for all styles:

```
1. Do this.
3. Done.
```

This rule supports 0-prefixing ordered list items for uniform indentation:

```
...
08. Item
09. Item
10. Item
11. Item
...
```

Note: This rule will report violations for cases like the following where an improperly-indented code block (or similar) appears between two list items and "breaks" the list in two:

```
1. First list

​```text
Code block
​```

1. Second list
```

The fix is to indent the code block so it becomes part of the preceding list item as intended:

```
1. First list

   ```text
   Code block
   ```

2. Still first list
```

Rationale: Consistent formatting makes it easier to understand a document.



## MD030 - Spaces after list markers

Tags: ol, ul, whitespace

Aliases: list-marker-space

Parameters: ul_single, ol_single, ul_multi, ol_multi (number; default 1)

This rule checks for the number of spaces between a list marker (e.g. '`-`', '`*`', '`+`' or '`1.`') and the text of the list item.

The number of spaces checked for depends on the document style in use, but the default is 1 space after any list marker:

```
* Foo
* Bar
* Baz

1. Foo
1. Bar
1. Baz

1. Foo
   * Bar
1. Baz
```

A document style may change the number of spaces after unordered list items and ordered list items independently, as well as based on whether the content of every item in the list consists of a single paragraph, or multiple paragraphs (including sub-lists and code blocks).

For example, the style guide at https://cirosantilli.com/markdown-style-guide#spaces-after-list-marker specifies that 1 space after the list marker should be used if every item in the list fits within a single paragraph, but to use 2 or 3 spaces (for ordered and unordered lists respectively) if there are multiple paragraphs of content inside the list:

```
* Foo
* Bar
* Baz

```

vs.

```

*   Foo

    Second paragraph

*   Bar
```

or

```
1.  Foo

    Second paragraph

1.  Bar
```

To fix this, ensure the correct number of spaces are used after list marker for your selected document style.

Rationale: Violations of this rule can lead to improperly rendered content.



## MD031 - Fenced code blocks should be surrounded by blank lines

Tags: code, blank_lines

Aliases: blanks-around-fences

Parameters: list_items (boolean; default true)

This rule is triggered when fenced code blocks are either not preceded or not followed by a blank line:

```
Some text
​```
Code block
​```

​```
Another code block
​```
Some more text
```

To fix this, ensure that all fenced code blocks have a blank line both before and after (except where the block is at the beginning or end of the document):

```
Some text

​```
Code block
​```

​```
Another code block
​```

Some more text
```

Set the `list_items` parameter to `false` to disable this rule for list items. Disabling this behavior for lists can be useful if it is necessary to create a [tight](https://spec.commonmark.org/0.29/#tight) list containing a code fence.

Rationale: Aside from aesthetic reasons, some parsers, including kramdown, will not parse fenced code blocks that don't have blank lines before and after them.



## MD032 - Lists should be surrounded by blank lines

Tags: bullet, ul, ol, blank_lines

Aliases: blanks-around-lists

This rule is triggered when lists (of any kind) are either not preceded or not followed by a blank line:

```
Some text
* Some
* List

1. Some
2. List
Some text
```

To fix this, ensure that all lists have a blank line both before and after (except where the block is at the beginning or end of the document):

```
Some text

* Some
* List

1. Some
2. List

Some text
```

Rationale: Aside from aesthetic reasons, some parsers, including kramdown, will not parse lists that don't have blank lines before and after them.



## MD033 - Inline HTML

Tags: html

Aliases: no-inline-html

Parameters: allowed_elements (array of string; default empty)

This rule is triggered whenever raw HTML is used in a markdown document:

```
<h1>Inline HTML heading</h1>
```

To fix this, use 'pure' markdown instead of including raw HTML:

```
# Markdown heading
```

Note: To allow specific HTML elements, use the 'allowed_elements' parameter.

Rationale: Raw HTML is allowed in markdown, but this rule is included for those who want their documents to only include "pure" markdown, or for those who are rendering markdown documents in something other than HTML.

## MD034 - Bare URL used

Tags: links, url

Aliases: no-bare-urls

This rule is triggered whenever a URL is given that isn't surrounded by angle brackets:

```
For more information, see https://www.example.com/.
```

To fix this, add angle brackets around the URL:

```
For more information, see <https://www.example.com/>.
```

Note: To use a bare URL without it being converted into a link, enclose it in a code block, otherwise in some markdown parsers it *will* be converted:

```
`https://www.example.com`
```

Note: The following scenario does *not* trigger this rule to avoid conflicts with `MD011`/`no-reversed-links`:

```
[https://www.example.com]
```

The use of quotes around a bare link will *not* trigger this rule, either:

```
"https://www.example.com"
'https://www.example.com'
```

Rationale: Without angle brackets, the URL isn't converted into a link by many markdown parsers.



## MD035 - Horizontal rule style

Tags: hr

Aliases: hr-style

Parameters: style ("consistent", "---", "***", or other string specifying the horizontal rule; default "consistent")

This rule is triggered when inconsistent styles of horizontal rules are used in the document:

```
---

- - -

***

* * *

****
```

To fix this, ensure any horizontal rules used in the document are consistent, or match the given style if the rule is so configured:

```
---

---
```

Note: by default, this rule is configured to just require that all horizontal rules in the document are the same, and will trigger if any of the horizontal rules are different than the first one encountered in the document. If you want to configure the rule to match a specific style, the parameter given to the 'style' option is a string containing the exact horizontal rule text that is allowed.

Rationale: Consistent formatting makes it easier to understand a document.



## MD036 - Emphasis used instead of a heading

Tags: headings, headers, emphasis

Aliases: no-emphasis-as-heading, no-emphasis-as-header

Parameters: punctuation (string; default ".,;:!?。，；：！？")

This check looks for instances where emphasized (i.e. bold or italic) text is used to separate sections, where a heading should be used instead:

```
**My document**

Lorem ipsum dolor sit amet...

_Another section_

Consectetur adipiscing elit, sed do eiusmod.
```

To fix this, use markdown headings instead of emphasized text to denote sections:

```
# My document

Lorem ipsum dolor sit amet...

## Another section

Consectetur adipiscing elit, sed do eiusmod.
```

Note: This rule looks for single line paragraphs that consist entirely of emphasized text. It won't fire on emphasis used within regular text, multi-line emphasized paragraphs, or paragraphs ending in punctuation (normal or full-width). Similarly to rule MD026, you can configure what characters are recognized as punctuation.

Rationale: Using emphasis instead of a heading prevents tools from inferring the structure of a document. More information: https://cirosantilli.com/markdown-style-guide#emphasis-vs-headers.



## MD037 - Spaces inside emphasis markers

Tags: whitespace, emphasis

Aliases: no-space-in-emphasis

This rule is triggered when emphasis markers (bold, italic) are used, but they have spaces between the markers and the text:

```
Here is some ** bold ** text.

Here is some * italic * text.

Here is some more __ bold __ text.

Here is some more _ italic _ text.
```

To fix this, remove the spaces around the emphasis markers:

```
Here is some **bold** text.

Here is some *italic* text.

Here is some more __bold__ text.

Here is some more _italic_ text.
```

Rationale: Emphasis is only parsed as such when the asterisks/underscores aren't completely surrounded by spaces. This rule attempts to detect where they were surrounded by spaces, but it appears that emphasized text was intended by the author.



## MD038 - Spaces inside code span elements

Tags: whitespace, code

Aliases: no-space-in-code

This rule is triggered for code span elements that have spaces adjacent to the backticks:

```
`some text `

` some text`
```

To fix this, remove any spaces adjacent to the backticks:

```
`some text`
```

Note: A single leading and trailing space is allowed by the specification and automatically trimmed (to allow for embedded backticks):

```
`` `backticks` ``
```

Note: A single leading or trailing space is allowed if used to separate codespan markers from an embedded backtick:

```
`` ` embedded backtick``
```

Rationale: Violations of this rule can lead to improperly rendered content.



## MD039 - Spaces inside link text

Tags: whitespace, links

Aliases: no-space-in-links

This rule is triggered on links that have spaces surrounding the link text:

```
[ a link ](https://www.example.com/)
```

To fix this, remove the spaces surrounding the link text:

```
[a link](https://www.example.com/)
```

Rationale: Consistent formatting makes it easier to understand a document.



## MD040 - Fenced code blocks should have a language specified

Tags: code, language

Aliases: fenced-code-language

This rule is triggered when fenced code blocks are used, but a language isn't specified:

```
​```
#!/bin/bash
echo Hello world
​```
```

To fix this, add a language specifier to the code block:

```
​```bash
#!/bin/bash
echo Hello world
​```
```

Rationale: Specifying a language improves content rendering by using the correct syntax highlighting for code. More information: https://cirosantilli.com/markdown-style-guide#option-code-fenced.



## MD041 - First line in file should be a top level heading

Tags: headings, headers

Aliases: first-line-heading, first-line-h1

Parameters: level, front_matter_title (number; default 1, string; default "^\s*title:")

This rule is intended to ensure documents have a title and is triggered when the first line in the file isn't a top level (h1) heading:

```
This is a file without a heading
```

To fix this, add a top level heading to the beginning of the file:

```
# File with heading

This is a file with a top level heading
```

Note: The `level` parameter can be used to change the top level (ex: to h2) in cases where an h1 is added externally.

If [YAML](https://en.wikipedia.org/wiki/YAML) front matter is present and contains a `title` property (commonly used with blog posts), this rule will not report a violation. To use a different property name in front matter, specify the text of a regular expression via the `front_matter_title` parameter. To disable the use of front matter by this rule, specify `""` for `front_matter_title`.

Rationale: The top level heading often acts as the title of a document. More information: https://cirosantilli.com/markdown-style-guide#top-level-header.



## MD042 - No empty links

Tags: links

Aliases: no-empty-links

This rule is triggered when an empty link is encountered:

```
[an empty link]()
```

To fix the violation, provide a destination for the link:

```
[a valid link](https://example.com/)
```

Empty fragments will trigger this rule:

```
[an empty fragment](#)
```

But non-empty fragments will not:

```
[a valid fragment](#fragment)
```

Rationale: Empty links do not lead anywhere and therefore don't function as links.



## MD043 - Required heading structure

Tags: headings, headers

Aliases: required-headings, required-headers

Parameters: headings, headers (array of string; default `null` for disabled)

> If `headings` is not provided, `headers` (deprecated) will be used.

This rule is triggered when the headings in a file do not match the array of headings passed to the rule. It can be used to enforce a standard heading structure for a set of files.

To require exactly the following structure:

```
# Head
## Item
### Detail
```

Set the `headings` parameter to:

```
[
    "# Head",
    "## Item",
    "### Detail"
]
```

To allow optional headings as with the following structure:

```
# Head
## Item
### Detail (optional)
## Foot
### Notes (optional)
```

Use the special value `"*"` meaning "one or more unspecified headings" and set the `headings` parameter to:

```
[
    "# Head",
    "## Item",
    "*",
    "## Foot",
    "*"
]
```

When an error is detected, this rule outputs the line number of the first problematic heading (otherwise, it outputs the last line number of the file).

Note that while the `headings` parameter uses the "## Text" ATX heading style for simplicity, a file may use any supported heading style.

Rationale: Projects may wish to enforce a consistent document structure across a set of similar content.



## MD044 - Proper names should have the correct capitalization

Tags: spelling

Aliases: proper-names

Parameters: names, code_blocks (string array; default `null`, boolean; default `true`)

This rule is triggered when any of the strings in the `names` array do not have the specified capitalization. It can be used to enforce a standard letter case for the names of projects and products.

For example, the language "JavaScript" is usually written with both the 'J' and 'S' capitalized - though sometimes the 's' or 'j' appear in lower-case. To enforce the proper capitalization, specify the desired letter case in the `names` array:

```
[
    "JavaScript"
]
```

Set the `code_blocks` parameter to `false` to disable this rule for code blocks.

Rationale: Incorrect capitalization of proper names is usually a mistake.



## MD045 - Images should have alternate text (alt text)

Tags: accessibility, images

Aliases: no-alt-text

This rule is triggered when an image is missing alternate text (alt text) information.

Alternate text is commonly specified inline as:

```
![Alternate text](image.jpg)
```

Or with reference syntax as:

```
![Alternate text][ref]

...

[ref]: image.jpg "Optional title"
```

Guidance for writing alternate text is available from the [W3C](https://www.w3.org/WAI/alt/), [Wikipedia](https://en.wikipedia.org/wiki/Alt_attribute), and [other locations](https://www.phase2technology.com/blog/no-more-excuses-definitive-guide-alt-text-field).

Rationale: Alternate text is important for accessibility and describes the content of an image for people who may not be able to see it.



## MD046 - Code block style

Tags: code

Aliases: code-block-style

Parameters: style ("consistent", "fenced", "indented"; default "consistent")

This rule is triggered when unwanted or different code block styles are used in the same document.

In the default configuration this rule reports a violation for the following document:

```
Some text.

    # Indented code

More text.

​```ruby
# Fenced code
​```

More text.
```

To fix violations of this rule, use a consistent style (either indenting or code fences).

The specified style can be specific (`fenced`, `indented`) or simply require that usage be consistent within the document (`consistent`).

Rationale: Consistent formatting makes it easier to understand a document.



## MD047 - Files should end with a single newline character

Tags: blank_lines

Aliases: single-trailing-newline

This rule is triggered when there is not a single newline character at the end of a file.

Example that triggers the rule:

```
# Heading

This file ends without a newline.[EOF]
```

To fix the violation, add a newline character to the end of the file:

```
# Heading

This file ends with a newline.
[EOF]
```

Rationale: Some programs have trouble with files that do not end with a newline. More information: https://unix.stackexchange.com/questions/18743/whats-the-point-in-adding-a-new-line-to-the-end-of-a-file.



## MD048 - Code fence style

Tags: code

Aliases: code-fence-style

Parameters: style ("consistent", "tilde", "backtick"; default "consistent")

This rule is triggered when the symbols used in the document for fenced code blocks do not match the configured code fence style:

```
​```ruby
# Fenced code
​```

~~~ruby
# Fenced code
~~~
```

To fix this issue, use the configured code fence style throughout the document:

```
​```ruby
# Fenced code
​```

​```ruby
# Fenced code
​```
```

The configured list style can be a specific symbol to use (backtick, tilde), or can require that usage be consistent within the document.

Rationale: Consistent formatting makes it easier to understand a document.