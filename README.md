# mml(Minimalist)

[![Hugo](https://img.shields.io/badge/hugo-0.74.3-blue.svg)](https://gohugo.io)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

### A blog theme for [Hugo](https://gohugo.io).

![Screenshot](https://raw.githubusercontent.com/Cluas/mml/master/images/Screenshot.png)


**This project is based on
[LeaveIt](https://raw.githubusercontent.com/liuzc/LeaveIt/)**

Because the author of
[LeaveIt](https://raw.githubusercontent.com/liuzc/LeaveIt/) seems to have
abandoned this project, but I prefer this theme, so I simply reopened a new
project.

At this stage, I mainly integrate the part I modified with LeaveIt, and will add
more features in the future.

## Features

- Images lazy loading
  ([Can I use?](https://caniuse.com/#search=Lazy%20loading%20via%20attribute%20for%20images%20%26%20iframes))
- Automatically highlighting code (Support by
  [highlight.js](https://highlightjs.org/))
- TeX Functions (Support by [KaTeX](https://katex.org/))
- [PlantUML](https://plantuml.com/en/) (Sequence diagram, Usecase diagram, Class
  diagram ...)
- Dark/Light Mode
- Support for embedded BiliBili video
- Support hidden text ...
            

## Requirements

Hugo 0.74.3 or higher

**Hugo extended version**, read more
[here](https://gohugo.io/news/0.48-relnotes/)

## Installation

Navigate to your hugo project root and run:

```console
git submodule add https://github.com/Cluas/mml themes/mml
```

Then run hugo (or set `theme: mml` in configuration file)

```console
hugo server --minify --theme mml
```

## Creating site from scratch

Below is example how to create new site from scratch

```console
hugo new site mydocs; cd mydocs
git init
git submodule add https://github.com/Cluas/mml  themes/mml
cp -R themes/mml/exampleSite/content .
```

```console
hugo server --minify --theme mml
```

## Lazy loading

If your browser is
[supported](https://caniuse.com/#search=Lazy%20loading%20via%20attribute%20for%20images%20%26%20iframes),
we will lazy loading `<img>` and `<iframes>`

Make sure your browser version:

- Chrome > 76
- Firefox > 75

## TeX Functions

**Note:**
[list of TeX functions supported by KaTeX](https://katex.org/docs/supported.html)

To enable KaTex globally set the parameter `math` to `true` in a project's
`config.toml`

To enable KaTex on a per page basis include the parameter `math: true` in
content files.

### Example

```latex
% Inline math:
$$ \varphi = \dfrac{1+\sqrt5}{2}= 1.6180339887… $$

% or
% Block math:
$$
 \varphi = 1+\frac{1} {1+\frac{1} {1+\frac{1} {1+\cdots} } }
$$
```

![KaTeX](https://raw.githubusercontent.com/Cluas/mml/master/images/KaTeX.png)

## PlantUML

**PlantUML is supported by the
[official server](https://www.plantuml.com/plantuml/uml/SyfFKj2rKt3CoKnELR1Io4ZDoSa70000)**

To enable KaTex globally set the parameter `plantuml` to `true` in a project's
`config.toml`

To enable KaTex on a per page basis include the parameter `plantuml: true` in
content files.

You can insert PlantUML in the post by:

<pre>
&#96;&#96;&#96;plantuml
PlantUML syntax
&#96;&#96;&#96;
</pre>

For example:

```plantuml
@startuml
Bob -> Alice : hello

create Other
Alice -> Other : new

create control String
Alice -> String
note right : You can also put notes!

Alice --> Bob : ok

@enduml
```

![PlantUML](https://raw.githubusercontent.com/Cluas/mml/master/images/PlantUML.svg)

## Embedded BiliBili video

You can embed BiliBili videos via Shortcodes, just provide the AV no./BV no. of
the bilibili video

You can also use the PV no. to control the PV no. (default: `1`)

```txt
{{< bilibili [AV number/BV number] [PVnumber] >}}
```


## Hidden text

You can use "hidden text" to hide spoiler content

```txt
{{< spoiler >}} HIDDEN TEXT {{< /spoiler >}}
```


## Gitalk comment system

This blog supports the [gitalk](https://github.com/gitalk/gitalk) comment
system. To use gitalk, you need to apply for a Github Application. 

enable gitalk in config.toml

```toml
[params]
    enableGitalk = true
```

Then provide your `Client ID` and `Client Secret` from Github Application in
config.toml

```toml
[params.gitalk] # Github: https://github.com/gitalk/gitalk
    clientID = "[Client ID]" # Your client ID
    clientSecret = "[Client Secret]" # Your client secret
    repo = "" # The repo to store comments
    owner = "" # Your GitHub ID
    admin= "" # Required. Github repository owner and collaborators. (Users who having write access to this repository)
    id= "location.pathname" # The unique id of the page.
    labels= "gitalk" # Github issue labels. If you used to use Gitment, you can change it
    perPage= 15 # Pagination size, with maximum 100.
    pagerDirection= "last" # Comment sorting direction, available values are 'last' and 'first'.
    createIssueManually= true # If it is 'false', it is auto to make a Github issue when the administrators login.
    distractionFreeMode= false # Enable hot key (cmd|ctrl + enter) submit comment.
```

## Custom CSS/JavaScript

Support custom CSS or JavaScript

Place your custom CSS and JavaScript files in the `/static/css` and `/static/js`
directories of your blog, respectively

```txt
static
├── css
│   └── _custom.css
└── js
    └── _custom.js
```

Then edit in `config.toml`:

```toml
[params.custom]
    css = ["css/_custom.css"]
    js = ["js/_custom.js"]
```

*Currently only supports CSS does not support Sass*

## Configuration

There are few configuration options you can add to your `config.toml` file.

```toml
baseURL = "" # <head> 里面的 baseurl 信息，填你的博客地址
title = "" # 浏览器的标题
languageCode = "zh-cn" # 语言
hasCJKLanguage = true # 开启可以让「字数统计」统计汉字
theme = "mml" # 主题

paginate = 5 # 每页的文章数
enableEmoji = true # 支持 Emoji
enableRobotsTXT = true # 支持 robots.txt


preserveTaxonomyNames = true

[blackfriday]
  hrefTargetBlank = true
  nofollowLinks = true
  noreferrerLinks = true

[Permalinks]
  posts = "/:year/:filename/"

[menu]
  [[menu.main]]
    name = "Blog"
    url = "/post/"
    weight = 1

  [[menu.main]]
    name = "Categories"
    url = "/categories/"
    weight = 2

  [[menu.main]]
    name = "Tags"
    url = "/tags/"
    weight = 3

  [[menu.main]]
    name = "About"
    url = "/about/"
    weight = 4

[params]
    since = 2017
    author = ""                         # Author's name
    avatar = "/images/me/avatar.jpg"    # Author's avatar
    subtitle = ""                       # Subtitle
    home_mode = ""                      # post or other
    enableGitalk = true                 # gitalk 评论系统

    google_verification = ""

    description = "" # (Meta) 描述
    keywords = "" # site keywords

    beian = ""
    baiduAnalytics = ""
    googleAnalytics = "" # Google 统计 id

    license= '本文采用<a rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/" target="_blank">知识共享署名-非商业性使用 4.0 国际许可协议</a>进行许可'

[params.gitalk] # Github: https://github.com/gitalk/gitalk
    clientID = "" # Your client ID
    clientSecret = "" # Your client secret
    repo = "" # The repo to store comments
    owner = "" # Your GitHub ID
    admin= "" # Required. Github repository owner and collaborators. (Users who having write access to this repository)
    id= "location.pathname" # The unique id of the page.
    labels= "gitalk" # Github issue labels. If you used to use Gitment, you can change it
    perPage= 15 # Pagination size, with maximum 100.
    pagerDirection= "last" # Comment sorting direction, available values are 'last' and 'first'.
    createIssueManually= true # If it is 'false', it is auto to make a Github issue when the administrators login.
    distractionFreeMode= false # Enable hot key (cmd|ctrl + enter) submit comment.

```

---

> The name of this project comes from **Minimalist** m m l
