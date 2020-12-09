# 文档

* 方法
  - 记录
  - 整理
* 概念用文档整理
* 结构化用思维导图，不宜太详细

## 笔记

* 功能
  - 标签功能
  - 可以聚合统计
* [Paper](http://www.fiftythree.com/):优雅，美观，做笔记，记录灵感
* [语雀](https://www.yuque.com)
* [Google文档](https://docs.google.com/document/u/0/)
* [腾讯文档](https://docs.qq.com/)：对标Google docs
* youdaonote ：格式化笔记
* simplenote：简单笔记（无格式）
* xmind：结构化整理
* 豆瓣：书、电影评论
* Goole keep
* notes
* [OneNote](https://products.office.com/zh-CN/onenote)
* TickTick
* [石墨文档](https://shimo.im)
* [GitbookIO/gitbook](https://github.com/GitbookIO/gitbook):📝 Modern documentation format and toolchain using Git and Markdown https://www.gitbook.com
* [mkdocs/mkdocs](https://github.com/mkdocs/mkdocs):Project documentation with Markdown. http://www.mkdocs.org
* [laurent22/joplin](https://github.com/laurent22/joplin):Joplin - an open source note taking and to-do application with synchronization capabilities for Windows, macOS, Linux, Android and iOS. Forum: [Joplin Forum - Joplin Forum](https://discourse.joplinapp.org/) [https://joplinapp.org,需要自己搭建存储](https://joplinapp.org,%E9%9C%80%E8%A6%81%E8%87%AA%E5%B7%B1%E6%90%AD%E5%BB%BA%E5%AD%98%E5%82%A8)
  - `brew cask install joplin`
  - `wget -O - https://raw.githubusercontent.com/laurent22/joplin/master/Joplin_install_and_update.sh | bash`
* [P3X OneNote](link)： a cloud-based note-taking application and is considered as an exact alternative to the well known Microsoft OneNote application
* [Notion](./Notion.md)
* [Roam Research](https://roamresearch.com/)
* [Simple note](https://standardnotes.org):收费
* [Grace Note](https://grace-note.app/#/)
* [Obsidian](https://obsidian.md/):A second brain, for you, forever.
* evernote
  - dunk
* [vnote](https://github.com/tamlok/vnote)A note-taking application that knows programmers and Markdown better.

## PPT

* [slideshare](https://www.slideshare.net/):Share what you know and love through presentations, infographics, documents and more
* [jxnblk/mdx-deck](https://github.com/jxnblk/mdx-deck):MDX-based presentation decks

## Posters

* [corkami/pics](https://github.com/corkami/pics):Posters, drawings...

## [asciidoctor/asciidoctor](https://github.com/asciidoctor/asciidoctor)

💎 A fast, open source text processor and publishing toolchain, written in Ruby, for converting AsciiDoc content to HTML5, DocBook 5 (or 4.5) and other formats. https://asciidoctor.org

```sh
gem install asciidoctor

gem install asciidoctor-diagram
sudo apt-get intall openjdk-8-jre-headless  install graphviz

asciidoctor -r asciidoctor-diagram xxx.adoc
```

## [jgm/pandoc](https://github.com/jgm/pandoc)

Universal markup converter http://johnmacfarlane.net/pandoc John MacFarlane开发的标记语言转换工具，可实现不同标记语言间的格式转换.

* 将Markdown转化为Word，然后统计字数
* [文档](http://pandoc.org/getting-started.html)

```sh
pandoc WEB.md -o web.docx
pandoc API.md -o api.docx -c Github.css
```

## [GitbookIO/gitbook](https://github.com/GitbookIO/gitbook)

📝 Modern documentation format and toolchain using Git and Markdown [GitBook - Document Everything!](https://www.gitbook.com)

* gitbook --version：查看当前使用的版本
* gitbook ls：系统存在的 gitbook 版本
* gitbook ls-remote：所有 gitbook 版本
* gitbook fetch：下载对应的 gitbook 版本
* gitbook current：当前目录使用的 gitbook 版本
* 使用
  - gitbook init 创建项目，生成
    + README.md
    + SUMMARY.md:定义书籍的章节的，用来生成目录
  - gitbook serve 运行
  - gitbook build 编译书籍

```
# Summary
- [Introduction](README.md)
# 一级分类，不显示，会以横线分隔，相当于注释
- [Introduction](part1/README.md)
- [Part1 Section 1](part1/section-1.md)
- [Part1 Section 2](part1/subsection-x/README.md)
    - [Part1 Section 2-1](part1/subsection-x/subsection-x-1.md)
    - [Part1 Section 2-2](part1/subsection-x/subsection-x-2.md)
# 一级分类，不显示，会以横线分隔，相当于注释
- [Introduction](part2/README.md)
- [part2 Section 1](part2/section-1.md)
- 未完成的时候
    - [part2 Section 2-1](part2/subsection-x/subsection-x-1.md)
    - [part2 Section 2-2](part2/subsection-x/subsection-x-2.md)
## 二级分类，显示，不可点
- An article in part 2
### 三级分类，显示，不可点，和二级效果一致
- An article in part 3
# 一级分类，不显示，会以横线分隔
- An article in an untitled part
```

```json
# 配置文件book.json
"pluginsConfig": {
  #展示章节硬编码
 "theme-default": {
     "showLevel": true
 }
}
```

## [deepnote](https://deepnote.com/)

a new kind of data science notebook. Jupyter-compatible with real-time collaboration and easy deployment. Oh, and it's free

## pdf

* [paperplane](https://www.paperplane.app/):High quality HTML to PDF conversion API for developers

## 工具

* [coolwanglu/pdf2htmlEX](https://github.com/coolwanglu/pdf2htmlEX):Convert PDF to HTML without losing text or format. http://coolwanglu.github.com/pdf2htmlEX/
* [peachdocs/peach](https://github.com/peachdocs/peach):Peach is a web server for multi-language, real-time synchronization and searchable documentation. https://peachdocs.org
* [Kozea/WeasyPrint](https://github.com/Kozea/WeasyPrint):WeasyPrint converts web documents (HTML with CSS, SVG, …) to PDF. https://weasyprint.org/
* [basecamp/trix](https://github.com/basecamp/trix):A rich text editor for everyday writing https://trix-editor.org/
* [leptosia/docute](https://github.com/leptosia/docute):📜 Effortlessly documentation done right. https://docute.org
* [acebook/Docusaurus](https://github.com/facebook/Docusaurus):Easy to maintain open source documentation websites. https://docusaurus.io
* [open-xml-templating/docxtemplater](https://github.com/open-xml-templating/docxtemplater):Generate docx and pptx (microsoft word documents) from templates, from Node.js, the Browser and the command line / Demo: https://docxtemplater.com/demo https://docxtemplater.com
* [mdx-js/mdx](https://github.com/mdx-js/mdx):JSX in Markdown for ambitious projects https://mdxjs.com
* [prezi](https://prezi.com/pricing/edu/)
* [linkedin/hopscotch](https://github.com/linkedin/hopscotch):A framework to make it easy for developers to add product tours to their pages.
* [gitpitch/gitpitch](https://github.com/gitpitch/gitpitch):The Markdown Presentation Service For Everyone on GitHub, GitLab, Bitbucket, GitBucket, Gitea, and Gogs. https://gitpitch.com
* [enquirer/enquirer](https://github.com/enquirer/enquirer):Stylish, intuitive and user-friendly prompt system.
* [sofish/typo.css](https://github.com/sofish/typo.css):中文网页重设与排版：一致化浏览器排版效果，构建最适合中文阅读的网页排版 http://typo.sofi.sh
* [unifiedjs/unified](https://github.com/unifiedjs/unified):☔ friendly interface backed by an ecosystem of plugins built for creating and manipulating content https://unified.js.org
* [docsifyjs/docsify](https://github.com/docsifyjs/docsify):🃏 A magical documentation site generator. https://docsify.js.org
* [mkdocs/mkdocs](https://github.com/mkdocs/mkdocs):Project documentation with Markdown. http://www.mkdocs.org
* [pedronauck/docz](https://github.com/pedronauck/docz):✍🏻It has never been so easy to document your things! https://docz.site
* [TryGhost/Ghost](https://github.com/TryGhost/Ghost):The platform for professional publishers https://ghost.org
* [gsuitedevs/md2googleslides](https://github.com/gsuitedevs/md2googleslides):Generate Google Slides from markdown
* [mailcow/mailcow-dockerized](https://github.com/mailcow/mailcow-dockerized):mailcow: dockerized - 🐮 + 🐋 = 💕 https://mailcow.email
* [mylxsw / wizard](https://github.com/mylxsw/wizard):Wizard是一款开源的文档管理工具，支持Markdown/Swagger/Table类型的文档。 http://wizard.aicode.cc

## 参考

* [What nobody tells you about documentation](https://www.divio.com/blog/documentation/)
* [myslide](https://myslide.cn)
