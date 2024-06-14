# MkDocs 使用教程

For full documentation visit [mkdocs.org](https://www.mkdocs.org).

## Commands
* `mkdocs new .` - Create a new project.
* `mkdocs serve` - Start the live-reloading docs server.
* `mkdocs build` - Build the documentation site.
* `mkdocs -h` - Print help message and exit.

## 1、Installation

```py
pip install mkdocs-material
```

## 2、Creating

```py
mkdocs new .
```

## 3、Configuration

```sh
??? note
    - `site_name`：网站的名称是 "MkDocs YouTube Tutorial"。
    - `site_url`：网站的 URL 是 https://james-willett.github.io/mkdocs-material-youtube-tutorial/。
    - `theme`：网站使用的主题是 Material 主题，配置了一些功能和配色方案。
      - `name`：主题名称为 Material。
      - `features`：包含了一系列功能，如导航、搜索等。
      - `language`：语言设置为英语。
      - `palette`：配色方案设置，包括两种方案，分别为默认的 teal 和 slate。
    - `plugins`：启用了一个社交插件，用于显示社交媒体链接。
    - `extra`：额外的配置信息，包括社交媒体的图标和链接。
    - `markdown_extensions`：Markdown 扩展，用于增强 Markdown 文档的功能，如代码高亮、注释、数学公式等。
    - `copyright`：版权信息，包括版权年份和作者信息。
    -   `features`：
        - navigation.sections         #启用了导航栏的章节功能，允许在导航栏中显示文档的章节结构。
        - toc.integrate               #允许用户快速浏览文档的结构和内容。
        - navigation.top              #启用了返回页面顶部的功能
        - search.suggest              #启用了搜索建议功能，当用户在搜索框中输入内容时，会显示相关的搜索建议，提高搜索的效率。
        - search.highlight            #启用了搜索结果高亮功能，搜索结果中匹配的关键词会被高亮显示。
        - content.tabs.link           #启用了内容区域的选项卡链接功能，允许在文档中创建多个选项卡，并在导航栏或其他位置添加链接以切换选项卡。
        - content.code.annotation     #启用了对代码块进行注释的功能，允许在代码块中添加注释或说明。
        - content.code.copy           #启用了复制代码块的功能，允许用户点击按钮或链接来复制代码块的内容到剪贴板。
```

```yaml
site_name: Markdown book
site_description: Describe what your site is about  # 设置文档网站的描述
site_url: 'https://example.com'  # 设置文档网站的 URL

theme:
  name: material
  language: en  # zh en
  palette:
    - scheme: default
      toggle:
        icon: material/toggle-switch-off-outline 
        name: Switch to dark mode
      primary: teal
      accent: purple 
    - scheme: slate 
      toggle:
        icon: material/toggle-switch
        name: Switch to light mode    
      primary: teal
  features:
    #- navigation.instant
    #- navigation.sections         #启用了导航栏的章节功能。
    #- toc.integrate               #允许用户快速浏览文档的结构和内容。
    - navigation.top              #启用了返回页面顶部的功能
    - search.suggest              #启用了搜索建议功能
    - search.highlight            #启用了搜索结果高亮功能。
    - content.tabs.link           #启用了内容区域的选项卡链接功能
    - content.code.annotation     #启用了对代码块进行注释的功能
    - content.code.copy           #启用了复制代码块的功能。

# Plugins
plugins:
  - blog
  - search:
      separator: '[\s\u200b\-_,:!=\[\]()"`/]+|\.(?!\d)|&[lg]t;|(?!\b)(?=[A-Z][a-z])'
  - minify:
      minify_html: true
  - offline

markdown_extensions:
  - pymdownx.highlight:
      anchor_linenums: true
  - pymdownx.inlinehilite
  - pymdownx.snippets
  - admonition
  - pymdownx.arithmatex:
      generic: true
  - footnotes
  - pymdownx.details
  - pymdownx.superfences
  - pymdownx.mark
  - attr_list
  - md_in_html
  - pymdownx.emoji:
      emoji_index: !!python/name:materialx.emoji.twemoji
      emoji_generator: !!python/name:materialx.emoji.to_svg

nav:  # 定义导航栏
  - Home: index.md  # 首页链接
  - Docker:
    - 01-MkDocs tutorial: 01-MkDocs tutorial.md  #
    - 02-Docker Commands: 02-Docker Commands.md  #
    - 03-Install Docker: 03-Install Docker.md  #
    - 04-Install Nginx: 04-Install Nginx.md  #
    - 05-Install Nextcloud: 05-Install Nextcloud.md  #
    - 06-SSH Remote Connection: 06-SSH Remote Connection.md  #
  - Colab: index.md 

```

## 4、Previewing as you write

```py
mkdocs serve
```

## 5、Build the documentation site

```py
mkdocs build
```

