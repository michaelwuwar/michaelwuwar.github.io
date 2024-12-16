---
author: ["Michael Wu"]
title: "如何简单快速搭建你的个人博客"
date: "2024-12-16"
description: "一站式解决搭建博客时遇到的问题，完成从创建项目到谷歌收录的流程"
summary: "一站式解决搭建博客时遇到的问题，完成从创建项目到谷歌收录的流程"
tags: ["blog", "papermod", "google", "hugo"]
categories: ["themes", "syntax"]
series: ["Blog Guide"]
ShowToc: true
TocOpen: true
---
### 写在开头

都点进这篇了，一定是想要搭建自己的博客。
如果你和我一样，对前端一窍不通，也不想在博客里整太多花哨效果，只希望有尽量简单浓缩的功能，那可以和我一样使用Hugo。
如果你去咨询程序猿朋友或者各种论坛，在中午互联网上大家基本都会推荐hexo，这个开源项目教程完善，插件多，并且重要的是**中文支持好**
但为什么还是推荐hugo呢？因为它快，它的自动部署非常快，同时其实框架完善程度不比hexo差，同时我也比较喜欢papermod这个主题的风格。
<del>当然不是因为我随便在github找到了这个<del>


### Inline Code

`This is Inline Code`

### Only `pre`

<pre>
This is pre text
</pre>

### Code block with backticks

```{hl_lines=[2,8]}
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <title>Example HTML5 Document</title>
    <meta
      name="description"
      content="Sample article showcasing basic Markdown syntax and formatting for HTML elements."
    />
  </head>
  <body>
    <p>Test</p>
  </body>
</html>
```

### Code block with backticks and language specified

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <title>Example HTML5 Document</title>
    <meta
      name="description"
      content="Sample article showcasing basic Markdown syntax and formatting for HTML elements."
    />
  </head>
  <body>
    <p>Test</p>
  </body>
</html>
```

### Code block with backticks and language specified with line numbers

```html {linenos=true}
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <title>Example HTML5 Document</title>
    <meta
      name="description"
      content="Sample article showcasing basic Markdown syntax and formatting for HTML elements."
    />
  </head>
  <body>
    <p>Test</p>
  </body>
</html>
```

### Code block with line numbers and <mark>highlighted</mark> lines

- PaperMod supports `linenos=true` or `linenos=table`

```html {linenos=true,hl_lines=[2,8]}
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <title>Example HTML5 Document</title>
    <meta
      name="description"
      content="Sample article showcasing basic Markdown syntax and formatting for HTML elements."
    />
  </head>
  <body>
    <p>Test</p>
  </body>
</html>
```

- <del>With `linenos=inline` line <mark>**might not** get highlighted</mark> properly.<del>
- This issue is fixed with [045c084](https://github.com/adityatelange/hugo-PaperMod/commit/045c08496d61b1b3f9c79e69e7d3d243a526d8f3)

```html {linenos=inline,hl_lines=[2,8]}
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <title>Example HTML5 Document</title>
    <meta
      name="description"
      content="Sample article showcasing basic Markdown syntax and formatting for HTML elements."
    />
  </head>
  <body>
    <p>Test</p>
  </body>
</html>
```

### Code block indented with four spaces

    <!doctype html>
    <html lang="en">
    <head>
      <meta charset="utf-8">
      <title>Example HTML5 Document</title>
    </head>
    <body>
      <p>Test</p>
    </body>
    </html>

### Code block with Hugo's internal highlight shortcode

{{< highlight html >}}

<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>Example HTML5 Document</title>
</head>
<body>
  <p>Test</p>
</body>
</html>
{{< /highlight >}}

### Github Gist

{{< gist adityatelange 376cd56ee2c94aaa2e8b93200f2ba8b5 >}}
