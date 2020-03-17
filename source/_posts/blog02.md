---
title: Config My Blog 02
date: 2020-03-05 14:05:38
categories: blog
tags:
- blog
- hexo
- hexo-icarus
---

## 前言
看到外星人的部落格主題 hexo-icarus 覺得太好看了，樣式全白、簡單、又有質感！於是花了幾天把主題從 hexo-next 改成 hexo-icarus，然後也有對其原先設定的 layout 做了一些修改。

<!--more-->

## 版面配置三欄
因為原本主題設定是有三個欄位，中間的欄位負責 display 文章，但看起來有點沒有重點，而且不夠 basic，所以把三欄改為兩欄。這邊其實蠻簡單的，就是去 icarus/\_config.yml 裡面把 widget 的 position 通通都設為 left，這樣原本在右邊的欄位就會通通跑到左邊來了。
其中我只留下幾個 widget，分別是 profile、toc、category、recent_posts、archive，其他都註解掉了。

## 版面比例
由於現在版面剩下兩欄，但其實左右兩側整個留空的比例還蠻高的，所以希望把這兩欄稍微往左右兩側擴展一些些。
這邊對 column == 2 時做了修改。

```ejs icarus/layout/layout.ejs
<% function main_column_class() {
    switch (column_count()) {
        case 1:
            return 'is-12';
        case 2:
            return 'is-8-tablet is-9-desktop is-9-widescreen';
        case 3:
            return 'is-8-tablet is-8-desktop is-6-widescreen'
    }
    return '';
} %>
```

```ejs icarus/layout/common/widget.ejs
<% function side_column_class() {
    switch (column_count()) {
        case 2:
            return 'is-4-tablet is-3-desktop is-3-widescreen';
        case 3:
            return 'is-4-tablet is-4-desktop is-3-widescreen';
    }
    return '';
} %>
```

把兩邊留空改小一點。
```css icarus/source/css/style.styl
gap = 15px
```

## 側邊欄近期文章
原先 sidebar 近期文章的顯示是標題+文章日期+文章類別+照片，但覺得這樣蠻多餘的，於是把照片跟類別拿掉，只留下最重要的資訊。
這邊註解了 image 的 block 以及 categories 的 block。（憑單詞註解:P）

```ejs icarus/layout/widget/recent_posts.ejs
<!--
    <p class="image is-64x64">
        <img class="thumbnail" src="<%= post.thumbnail %>" alt="<%= post.title %>">
    </p>
-->
    
<!--
    <p class="is-size-7 is-uppercase">
    <%- list_categories(post.categories(), {
    	show_count: false,
    	class: 'has-link-grey ',
    	depth:2,
    	style: 'none',
    	separator: ' / '}) %ʕ￫ᴥ￩ʔ>
    </p>
-->
```

## icarus/_config.yml 基本設定
1. 只打算留下 navigation bar 的 home、categories、about。（menu）
2. 把原本右上角連到 hexo-icarus github 的連結註解掉了。（links）
3. 網站右下角原先有三個連結也註解掉了。（footer）
4. 加入之前就有的留言/評論功能。（comment）
5. 註解 donation 的所有部分。(donate)

```yaml icarus/_config.yml
menu:
    #Home: /
    #Archives: /archives
    Categories: /categories
    #Tags: /tags
    About: /about

#links:
    #Download on GitHub:
    #icon: fab fa-github
    #url: 'https://github.com/ppoffice/hexo-theme-icarus'

#footer:
    # Links to be shown on the right of the footer section
    #links:
        #Creative Commons:
            #icon: fab fa-creative-commons
            #url: 'https://creativecommons.org/'
        #Attribution 4.0 International:
            #icon: fab fa-creative-commons-by
            #url: 'https://creativecommons.org/licenses/by/4.0/'
        #Download on GitHub:
            #icon: fab fa-github
            #url: 'https://github.com/ylkuo96' 

#donate:
    #-
        # Donation entry name
        #type: alipay
        # Qrcode image URL
        #qrcode: ''
    #-
        # Donation entry name
        #type: wechat
        # Qrcode image URL
        #qrcode: ''
    #-
        # Donation entry name
        #type: paypal
        # Paypal business ID or email address
        #business: ''
        # Currency code
        #currency_code: USD
    #-
        # Donation entry name
        #type: patreon
        # URL to the Patreon page
        #url: ''

comment:
    # Name of the comment plugin
    type: disqus
    shortname: yilin-comments
```

## 關於我
這邊多創建了一個分頁，大概就是要介紹我自己的意思 XD！不過我還沒寫完，只是先擺著放而已 :P。
`$ hexo new page about`

然後把評論功能關掉，只想開放文章的留言功能而已。
```markdown blog/source/about/index.md
---
title: About me
date: 2020-03-04 17:43:57
type: "about"
comment: false
---

<<待補充 :P>>
```

## favicon
關於網站的 icon （分頁上的 icon），把它換成覺得很有質感的線條。
用[此網站](https://favicon.io/favicon-generator/)製作而成的。
這個線條叫做 wavy dash。
{% img /uploads/images/blog02/icon.png 32 'favicon' %}

## 熊 logo
```ejs icarus/layout/common/navbar.ejs
<a class="navbar-item navbar-logo" href="<%- url_for('/') %>">
<% if (logo && logo.text) { %>
    <img src="/images/bear.svg" style="display:block;width:25px;height:25px" />
    <%= logo.text %>
<% } else { %>
    <img src="<%- url_for(logo) %>" alt="<%= title %>" height="28">
<% } %>
</a>
```

多加了第三行的 `<img src ... >`，其中 bear.svg 被放置在 icarus/source/images/。
完成之後會顯示如下圖。
{% img /uploads/images/blog02/bear.png 250 'bear logo' %}

超級無敵可愛的 logo 啊！！！！！連結點[此](https://www.flaticon.com/free-icon/teddy-bear_1943200)。

最後順便改了一下 blog/source/about/index.md，標示一下此 logo 的 author。

## References
1. [外星人部落格](https://oalieno.github.io/)
2. [logo](https://www.flaticon.com/)
