---
title: Config My Blog 01
date: 2020-03-03 16:11:20
categories: blog
keywords: blog
tags:
- blog
- github
- hexo
- hexo-next
---

## 前言
最近看很多大神同學都推薦 hexo 這個 Blog 框架，一時興起想說那就來寫一下 blog 吧！記得之前只有在國高中的時候用過無名寫過文章，還蠻好奇以前的自己究竟寫了什麼東西 XD。因為覺得最近的自己腦袋蠻空泛的，希望藉著寫一些部落格文章來 refresh 一下，同時也記錄各種生活中的大小事。

這次使用了 Hexo 這個 blog 框架。

<!--more-->

## Prerequisite
1. Node.js
2. Git

## Installation
`$ npm install -g hexo-cli`

## Create a blog
建立 hexo directory、並在此 directory 安裝好 npm 套件。
```
$ hexo init blog
$ cd blog
$ npm install
```

## Components
> 待補充完整

\_config.yml
- 網頁的整個配置設定。

source/
- \_posts 是放部落格文章的地方。

themes/
- blog 的主題樣式。

## Config
### Theme
設置部落格主題為 next。
```
$ cd blog
$ git clone https://github.com/theme-next/hexo-theme-next themes/next
```

其中有四種 schema 可以選。
在 theme 中的 \_config.yml 搜尋 scheme 選擇想要的即可，在這邊選擇了 Pisces。

其中 code highlight theme 也可以選。
我選擇將 `highlight_theme: normal` 改成 `highlight_theme: night eighties`。

在 theme 的 \_config.yml 中把 social 的 github 打開、並且 enable social icon only。把 lazyload 設為 true、把 toc 設為 false（文章目錄拔掉）、把 updated_at 設為 false（編輯文章的時間拔掉）。

最後在 blog 的 \_config.yml 將 `theme: landscape` 改成 `theme: next` 即可。


### Categories
寫文章前先建立 blog 的 "分類"。之後寫文章時可以把文章歸類。
```
$ hexo new page Categories
```

就可以去 /blog/source/Categories/index.md 編輯。
增加頁面的 type 屬性為 "categories"。
可以把頁面的 comments 關閉。
```
---
title: Categories
date: 2019-03-19 12:12:12
type: "categories"
comments: false
---
```

再來，就去 theme 的 \_config.yml 編輯，把前方 categories 的註解\#拿掉。我這邊也順便把 archives 加上註解 :P。
```
menu:
home: / || home
#about: /about/ || user
#tags: /tags/ || tags
categories: /categories/ || th
#archives: /archives/ || archive
#schedule: /schedule/ || calendar
#sitemap: /sitemap.xml || sitemap
#commonweal: /404/ || heartbeat
```

### Disqus
Disqus 這個 plugin 為文章加入了留言的功能。
1. 先去 [Disqus](https://disqus.com/) 申請帳號。
2. 申請 site。
3. 到 site 的 settings 點進 general 查看自己 website 的 shortname。
4. 修改 theme 的 \_config.yml。
```
disqus:
enable: true
shortname: {{shortname}}
count: true 
```

## Writing Post
首先建立新的文章。
``` 
$ cd blog
$ hexo new blog01 
```

就可以進去 /blog/source/_posts/blog01.md 編輯文章。
最前面的是一些基本資訊，關於文章標題、分類、標籤等等。
```
---
title: {{標題}}
date: {{創立時間}}
categories: {{分類}}
keywords: {{關鍵字}}
tags:
- {{tag1}}
- {{tag2}}
- {{tag3}}
---
```

接著就剩下文章內容的部分了，要自行發揮 :P。

## Preview and Deploy
設定完環境、寫完文章之後，啟動 local server。
```
$ cd blog
$ hexo server
```

即可在 http://localhost:4000 看到自己的部落格預覽的樣子。
（其實隨時在修改 blog 時就可以隨時開著頁面預覽了 :P）
{% img /uploads/images/blog01/preview.png 800 'preview blog' %}

確認預覽的頁面為自己想要的樣子之後，接著就要 deploy 到 github page 上了。

首先修改 blog 的 \_config.yml。
```
language: zh-tw

url: https://ylkuo96.github.io/

deploy: 
  type: git
  repo: https://github.com/ylkuo96/ylkuo96.github.io.git
  branch: master

```

部屬前要先安裝套件。
```
$ cd blog
$ npm install hexo-deployer-git --save
```

接著執行下列指令。
```
$ cd blog
$ hexo deploy
```

note:: 若遇到 `fatal: Not a git repository (or any of the parent directories): .git`，將 blog 底下的 .deploy_git 資料夾刪掉然後重新 deploy 即可。

完成之後即可在 https://ylkuo96.github.io 上看到自己的 blog！

## Summary
1. 新文章就 `$ hexo new <postname>`
2. 新分頁就 `$ hexo new page <pagename>`
3. 產生靜態檔 `$ hexo g` (generate)
4. 預覽 `$ hexo s` (server)
5. 部屬 `$ hexo d` (deploy) 
6. 若有點怪怪的可以時不時 `$ hexo clean` 一下 :P

## References
1. [other people's hexo blog](https://www.larrynote.com/website-service/6590/)
2. [用 git 維持 hexo 資料夾](https://github.com/LeonWuV/FE-blog-repository/blob/master/hexo/hexo%E7%B3%BB%E5%88%97%E9%97%AE%E9%A2%98%E4%B9%8B%E6%88%91%E4%BB%AC%E6%8D%A2%E4%BA%86%E7%94%B5%E8%84%91%E6%80%8E%E4%B9%88%E5%8A%9E.md)
3. [若 hexo g 報錯](http://blog.senjoeson.com/2018/06/07/hexo%E5%B8%B8%E7%94%A8%E9%97%AE%E9%A2%98%E8%A7%A3%E5%86%B3%E5%8A%9E%E6%B3%95/)
