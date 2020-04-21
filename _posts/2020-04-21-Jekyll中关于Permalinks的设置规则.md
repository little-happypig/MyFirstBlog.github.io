---
layout:     post
title:      2020-04-21-Jekyll中关于Permalinks的设置规则
subtitle:   
date:       2020-04-21 10:13:00
author:     BY 快乐小猪
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - Jekyll
    - Permalinks
    - 设置
---

# 永久链接

Jekyll 支持以灵活的方式管理你网站的链接，你可以通过 [Configuration](http://jekyllcn.com/docs/configuration/) 或 [YAML 头信息](http://jekyllcn.com/docs/frontmatter/) 为每篇文章设置永久链接。你可以随心所欲地选择内建链接格式，或者自定义链接格式。默认配置为 `date`。

永久链接的模板用以冒号为前缀的关键词标记动态内容，比如 `date` 代表 `/:categories/:year/:month/:day/:title.html`。

## [模板变量](http://jekyllcn.com/docs/permalinks/#模板变量)

| 变量         | 描述                                                         |
| ------------ | ------------------------------------------------------------ |
| `year`       | 文章文件名中的年份，格式如 `2013`                            |
| `month`      | 文章文件名中的月份，格式如 `01`                              |
| `i_month`    | 文章文件名中的月份，不包含首位的零，格式如 `1`               |
| `day`        | 文章文件名中的日期，格式如 `08`                              |
| `i_day`      | 文章文件名中的日期，不包含首位的零，格式如 `8`               |
| `short_year` | 文章文件名中的年份，后两位，格式如 `13`                      |
| `hour`       | 时钟，24 小时制，日期以文章的头信息中的 `date` 为基准。（00..23） |
| `minute`     | 当前时钟内的分钟，日期以文章的头信息中的 `date` 为基准。（00..59） |
| `second`     | 当前分钟内的秒钟，日期以文章的头信息中的 `date` 为基准。（00..59） |
| `title`      | 由文件的文件名中确定的标题，可以被文件头信息中的 `slug` 覆盖。 |
| `slug`       | 由文件的文件名中确定的　Slugified title（除数字和字母之外的字符们会被取代为连字符），可以被文件头信息中的 `slug` 覆盖。 |
| `categories` | 文章类型。如果一篇文章有多个类型，Jekyll 会创建一个目录（例如，`/category1/category2`）。Jekyll 也可以自动解析 URLs 中的双斜线 `//`，所以如果当前文章没有设定类型，则忽略该项。 |

## [内建永久链接类型](http://jekyllcn.com/docs/permalinks/#内建永久链接类型)

当你能够通过 [template variables](http://jekyllcn.com/docs/permalinks/#template-variables) 来指定一个自定义永久链接时，方便起见，Jekyll 还提供了下列的内建类型。

| 永久链接类型 | URL 模板                                     |
| ------------ | -------------------------------------------- |
| `date`       | `/:categories/:year/:month/:day/:title.html` |
| `pretty`     | `/:categories/:year/:month/:day/:title/`     |
| `ordinal`    | `/:categories/:year/:y_day/:title.html`      |
| `none`       | `/:categories/:title.html`                   |

## [页面（Pages） 和集合（collections）](http://jekyllcn.com/docs/permalinks/#页面pages-和集合collections)

`permalink` 配置用来指定博客的永久链接模板。页面和集合同样有它们自己的默认永久链接模板；页面的默认模板是 `/:path/:basename`，集合的默认模板是 /:collection/:path`。

这些样式被修改用来匹配在文章永久链接设置里的后缀式。例如，含有反斜杠 `/` 的永久链接模板 `pretty` 会更新页面的永久链接，使其同样包含一个反斜杠： `/:path/:basename/`。含有文件扩展名的永久链接模板 `date` 会更新页面的永久链接，使其同样包含文件扩展名： `/:path/:basename:output_ext`。这对任意自定义永久链接模板同样适用。

单独页面或集合文件的永久链接总能够在页面或者文件的[头信息](http://jekyllcn.com/docs/frontmatter/)里重写覆盖。另外，给定的集合的永久链接能在[集合配置](http://jekyllcn.com/docs/collections/)中自定义设置。

## [永久链接模板举例](http://jekyllcn.com/docs/permalinks/#永久链接模板举例)

比如文件名： `/2009-04-29-slap-chop.textile`

| URL 模板                                                     | 对应的永久链接 URL                      |
| ------------------------------------------------------------ | --------------------------------------- |
| 没有配置或 `permalink: date`                                 | `/2009/04/29/slap-chop.html`            |
| `pretty`                                                     | `/2009/04/29/slap-chop/`                |
| `/:month-:day-:year/:title.html`                             | `/04-29-2009/slap-chop.html`            |
| `/blog/:year/:month/:day/:title`                             | `/blog/2009/04/29/slap-chop/index.html` |
| `/:year/:month/:title`具体细节见于 [无扩展名链接（Extensionless permalinks）](http://jekyllcn.com/docs/permalinks/#extensionless-permalinks)。 | `/2009/04/slap-chop`                    |

## [无扩展名永久链接（Extensionless permalinks）](http://jekyllcn.com/docs/permalinks/#无扩展名永久链接extensionless-permalinks)

Jekyll 支持即不包含反斜杠也不包含文件扩展名的永久链接，但这需要网络服务端的额外支持才能正常工作。当使用无扩展名永久链接时，写到硬盘上的输出文件依然会保留正确的文件扩展名（典型的比如，`.html`），所以网络服务端必须能够 map 那些没有文件扩展名的文件的请求。

无论 [GitHub Pages](http://jekyllcn.com/docs/github-pages/) 还是 Jekyll 内置的 WEBrick server 都能够正确处理这些请求，不需要任何额外工作。

### [Apache](http://jekyllcn.com/docs/permalinks/#apache)

Apache 网络服务端对内容协商（content negotiation）有着非常广泛的支持，而且能够通过在你的 `httpd.conf` 或者 `.htaccess` 文件中设置 [multiviews](https://httpd.apache.org/docs/current/content-negotiation.html#multiviews) 选项来处理无扩展名的 URLs：

```
Options +MultiViews
```

### [Nginx](http://jekyllcn.com/docs/permalinks/#nginx)

[try_files](http://nginx.org/en/docs/http/ngx_http_core_module.html#try_files) 指令允许你指定一个文件列表搜索，用来处理请求。如果请求的 URL 的精确匹配未找到的的话，下列配置会让 nginx 搜索含有 `.html` 扩展名的文件。

```
try_files $uri $uri.html $uri/ =404;
```

[原文链接](http://jekyllrb.com/docs/permalinks/)

翻译贡献者

# 英文原文

# Permalinks

Permalinks are the output path for your pages, posts, or collections. They allow you to structure the directories of your source code different from the directories in your output.

## [Front Matter](https://www.jekyll.com.cn/docs/permalinks/#front-matter)

The simplest way to set a permalink is using front matter. You set the `permalink` variable in front matter to the output path you’d like.

For example, you might have a page on your site located at `/my_pages/about-me.html` and you want the output url to be `/about/`. In front matter of the page you would set:

```
---
permalink: /about/
---
```

## [Global](https://www.jekyll.com.cn/docs/permalinks/#global)

Setting a permalink in front matter for every page on your site is no fun. Luckily, Jekyll lets you set the permalink structure globally in your `_config.yml`.

To set a global permalink, you use the `permalink` variable in `_config.yml`. You can use placeholders to your desired output. For example:

```
permalink: /:categories/:year/:month/:day/:title:output_ext
```

Note that pages and collections (excluding `posts` and `drafts`) don’t have time and categories (for pages, the above `:title` is equivalent to `:basename`), these aspects of the permalink style are ignored for the output.

For example, a permalink style of `/:categories/:year/:month/:day/:title:output_ext` for the `posts` collection becomes `/:title.html` for pages and collections (excluding `posts` and `drafts`).

### [Placeholders](https://www.jekyll.com.cn/docs/permalinks/#placeholders)

Here’s the full list of placeholders available:

| VARIABLE        | DESCRIPTION                                                  |
| --------------- | ------------------------------------------------------------ |
| `year`          | Year from the post’s filename with four digits. May be overridden via the document’s `date` front matter. |
| `short_year`    | Year from the post’s filename without the century. (00..99) May be overridden via the document’s `date` front matter. |
| `month`         | Month from the post’s filename. (01..12) May be overridden via the document’s `date` front matter. |
| `i_month`       | Month without leading zeros from the post’s filename. May be overridden via the document’s `date` front matter. |
| `short_month`   | Three-letter month abbreviation, e.g. “Jan”.                 |
| `long_month`4.0 | Full month name, e.g. “January”.                             |
| `day`           | Day of the month from the post’s filename. (01..31) May be overridden via the document’s `date` front matter. |
| `i_day`         | Day of the month without leading zeros from the post’s filename. May be overridden via the document’s `date` front matter. |
| `y_day`         | Ordinal day of the year from the post’s filename, with leading zeros. (001..366) |
| `w_year`4.0     | Week year which may differ from the month year for up to three days at the start of January and end of December |
| `week`4.0       | Week number of the current year, starting with the first week having a majority of its days in January. (01..53) |
| `w_day`4.0      | Day of the week, starting with Monday. (1..7)                |
| `short_day`4.0  | Three-letter weekday abbreviation, e.g. “Sun”.               |
| `long_day`4.0   | Weekday name, e.g. “Sunday”.                                 |
| `hour`          | Hour of the day, 24-hour clock, zero-padded from the post’s `date` front matter. (00..23) |
| `minute`        | Minute of the hour from the post’s `date` front matter. (00..59) |
| `second`        | Second of the minute from the post’s `date` front matter. (00..59) |
| `title`         | Title from the document’s filename. May be overridden via the document’s `slug` front matter. |
| `slug`          | Slugified title from the document’s filename (any character except numbers and letters is replaced as hyphen). May be overridden via the document’s `slug` front matter. |
| `categories`    | The specified categories for this post. If a post has multiple categories, Jekyll will create a hierarchy (e.g. `/category1/category2`). Also Jekyll automatically parses out double slashes in the URLs, so if no categories are present, it will ignore this. |

### [Built-in formats](https://www.jekyll.com.cn/docs/permalinks/#built-in-formats)

For posts, Jekyll also provides the following built-in styles for convenience:

| PERMALINK STYLE | URL TEMPLATE                                             |
| --------------- | -------------------------------------------------------- |
| `date`          | `/:categories/:year/:month/:day/:title:output_ext`       |
| `pretty`        | `/:categories/:year/:month/:day/:title/`                 |
| `ordinal`       | `/:categories/:year/:y_day/:title:output_ext`            |
| `weekdate`4.0   | `/:categories/:year/W:week/:short_day/:title:output_ext` |
| `none`          | `/:categories/:title:output_ext`                         |

Rather than typing `permalink: /:categories/:year/:month/:day/:title/`, you can just type `permalink: pretty`.

#### Specifying permalinks through the front matter

Built-in permalink styles are not recognized in front matter. As a result, `permalink: pretty` will not work.

### [Collections](https://www.jekyll.com.cn/docs/permalinks/#collections)

For collections (including `posts` and `drafts`), you have the option to override the global permalink in the collection configuration in `_config.yml`:

```
collections:
  my_collection:
    output: true
    permalink: /:collection/:name
```

Collections have the following placeholders available:

| VARIABLE      | DESCRIPTION                                                  |
| ------------- | ------------------------------------------------------------ |
| `:collection` | Label of the containing collection.                          |
| `:path`       | Path to the document relative to the collection's directory, including base filename of the document. |
| `:name`       | The document's base filename, with every sequence of spaces and non-alphanumeric characters replaced by a hyphen. |
| `:title`      | The `:title` template variable will take the `slug` [front matter](https://www.jekyll.com.cn/docs/front-matter/) variable value if any is present in the document; if none is defined then `:title` will be equivalent to `:name`, aka the slug generated from the filename. |
| `:output_ext` | Extension of the output file. (Included by default and usually unnecessary.) |

### [Pages](https://www.jekyll.com.cn/docs/permalinks/#pages)

For pages, you have to use front matter to override the global permalink, and if you set a permalink via front matter defaults in `_config.yml`, it will be ignored.

Pages have the following placeholders available:

| VARIABLE      | DESCRIPTION                                                  |
| ------------- | ------------------------------------------------------------ |
| `:path`       | Path to the page relative to the site's source directory, excluding base filename of the page. |
| `:basename`   | The page's base filename                                     |
| `:output_ext` | Extension of the output file. (Included by default and usually unnecessary.) |
