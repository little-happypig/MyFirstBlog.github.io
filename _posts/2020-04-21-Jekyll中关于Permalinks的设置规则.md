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
# Permalinks

Permalinks are the output path for your pages, posts, or collections. They allow you to structure the directories of your source code different from the directories in your output.

## Front Matter[Permalink](https://www.jekyll.com.cn/docs/permalinks/#front-matter)

The simplest way to set a permalink is using front matter. You set the `permalink` variable in front matter to the output path you’d like.

For example, you might have a page on your site located at `/my_pages/about-me.html` and you want the output url to be `/about/`. In front matter of the page you would set:

```
---
permalink: /about/
---
```

## Global[Permalink](https://www.jekyll.com.cn/docs/permalinks/#global)

Setting a permalink in front matter for every page on your site is no fun. Luckily, Jekyll lets you set the permalink structure globally in your `_config.yml`.

To set a global permalink, you use the `permalink` variable in `_config.yml`. You can use placeholders to your desired output. For example:

```
permalink: /:categories/:year/:month/:day/:title:output_ext
```

Note that pages and collections (excluding `posts` and `drafts`) don’t have time and categories (for pages, the above `:title` is equivalent to `:basename`), these aspects of the permalink style are ignored for the output.

For example, a permalink style of `/:categories/:year/:month/:day/:title:output_ext` for the `posts` collection becomes `/:title.html` for pages and collections (excluding `posts` and `drafts`).

### Placeholders[Permalink](https://www.jekyll.com.cn/docs/permalinks/#placeholders)

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

### Built-in formats[Permalink](https://www.jekyll.com.cn/docs/permalinks/#built-in-formats)

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

### Collections[Permalink](https://www.jekyll.com.cn/docs/permalinks/#collections)

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

### Pages[Permalink](https://www.jekyll.com.cn/docs/permalinks/#pages)

For pages, you have to use front matter to override the global permalink, and if you set a permalink via front matter defaults in `_config.yml`, it will be ignored.

Pages have the following placeholders available:

| VARIABLE      | DESCRIPTION                                                  |
| ------------- | ------------------------------------------------------------ |
| `:path`       | Path to the page relative to the site's source directory, excluding base filename of the page. |
| `:basename`   | The page's base filename                                     |
| `:output_ext` | Extension of the output file. (Included by default and usually unnecessary.) |
