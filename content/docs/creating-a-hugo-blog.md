---
title: "Creating a Hugo blog"
date: 2019-05-11T21:38:49-07:00
draft: true
---

### Start the project
+ $ `hugo new site develedge`
+ $ `cd develedge`
+ $ `git init`

### Add the Theme
I am using [Kube](https://github.com/jeblister/kube/tree/master/layouts/partials)

+ $ `mkdir themes`
+ $ `cd themes`
+ $ `git clone https://github.com/jeblister/kube.git`
+ $ `echo 'theme = "kube"' >> config.toml`
+ $ `hugo server --theme=kube --buildDrafts --watch`
+ $ `vim config.toml`

```
baseURL = "/"
languageCode = "en-us"
title = "Developer Ledger"
theme = "kube"
description = "Resources by & for Jen Diamond"
Paginate = 10
[Params]
  RSSLink = "/index.xml"
  author = "Jen Diamond"
  github = "jendiamond"
  twitter = "jendiamond" 
  email = "thejendiamond@gmail.com"

[[menu.main]]
    name = "Docs"
    weight = -100
    url = "/docs/"
[[menu.main]]
    name = "Blog"
    weight = -100
    url = "/blog/"
[[menu.main]]
    name = "Faq"
    weight = -100
    url = "/faq/"

```

### [Archetypes](https://gohugo.io/content-management/archetypes/)
Archetypes are content template files in the archetypes directory of your project that contain preconfigured front matter and possibly also a content disposition for your website’s content types. These will be used when you run hugo new.

This will create a new content file in `content/posts/my-first-post.md` using the first archetype file found of these:
+ $ `hugo new posts/my-first-post.md`

1. archetypes/posts.md
1. archetypes/default.md
1. themes/my-theme/archetypes/posts.md
1. themes/my-theme/archetypes/default.md

(The last two list items are only applicable if you use a theme and it uses the my-theme theme name as an example.)

### Add single files
with "hugo new <SECTIONNAME>/<FILENAME>.<FORMAT>"  
+ $ `$ hugo new --kind docs docs/my-new-doc.md`  
The path to this file is `content/post/hugo_blog.md`

### Start the built-in live server via "hugo server"

+ $ `rm -rf public/`

### Styling
To add your own theme css or override existing CSS without having to change theme files do the following:
+ $ `vim themes/kube/static/css/custom.css`

---


---
+ $ ``
+ $ ``
+ $ ``
+ $ ``
+ $ ``
+ $ ``
+ $ ``
+ $ ``
+ $ ``
+ $ ``
+ $ ``
+ $ ``
+ $ ``