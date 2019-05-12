---
title: "Hugo_blog"
date: 2019-05-11T21:38:49-07:00
draft: true
---

+ $ `hugo new site develedge`
+ $ `cd develedge`
+ $ `git init`
+ $ `mkdir themes`
+ $ `cd themes`
+ $ `git clone https://github.com/jeblister/kube.git`
+ $ `echo 'theme = "kube"' >> config.toml`
+ $ `hugo server --theme=kube --buildDrafts --watch`
+ $ `vim config.toml`
```
baseURL = "https://example.org/"
languageCode = "en-us"
title = "Developer Ledger"
theme = "kube"

[author]
 author = "Jen Diamond"
 profile = "I am a software developer working in Los Angeles."
 image = 'image/theme/profile.jpg'

[Params]
 localeOgp = "en"
 description = "Jen Diamond's Resource blog"
 keywords = "samvera, blacklight"
 twitter = "jendiamond"
 github = "jendiamond"
```

### Add single files  
with "hugo new <SECTIONNAME>/<FILENAME>.<FORMAT>"  
+ $ `$ hugo new --kind docs docs/my-new-doc.md`  
The path to this file is `content/post/hugo_blog.md`

### Start the built-in live server via "hugo server"

+ $ `rm -rf public/`

### Stylingg
To add your own theme css or override existing CSS without having to change theme files do the following:
+ $ `vim themes/kube/static/css/custom.css`

---

### [Archetypes](https://gohugo.io/content-management/archetypes/)
Archetypes are content template files in the archetypes directory of your project that contain preconfigured front matter and possibly also a content disposition for your website’s content types. These will be used when you run hugo new.

This will create a new content file in `content/posts/my-first-post.md` using the first archetype file found of these:
+ $ `hugo new posts/my-first-post.md`

1. archetypes/posts.md
1. archetypes/default.md
1. themes/my-theme/archetypes/posts.md
1. themes/my-theme/archetypes/default.md

(The last two list items are only applicable if you use a theme and it uses the my-theme theme name as an example.)

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