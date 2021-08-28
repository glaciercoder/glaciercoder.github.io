---
layout: default
title:  "Welcome to Jekyll!"
date:   2021-08-28 18:55:39 +0800
categories: jekyll
---



## Background

This is my first blog stimulated by [suxy15](https://github.com/SuXY15), written to take down the prossess of writing blog using `Jeykll`

### Jekyll and Github Pages

Roughly speaking, Jekyll and Github Pages are two different parts. Jekyll is a static website generator like hexo(use html, mardown, etc to generate a new html), while Github Pages is a Github component which uses a repository to generate a user website. But Jekyll is the engine of Github Pages, which makes it convenient to set up a blog using Jekyll on Github. We just edit on our local machine, commit as usual and get our blog. 

### Basics

Basic information about Jekyll can be easily got from the [Jekyll official](https://jekyllrb.com/)

Set up Github Pages can see [Set up  Github Pages with Jekyll](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll)

### Some pitfalls

However, some pitfalls need to be noticed.

1. Theme changing

   There are different types of theme in Jekyll. For me, I use gem theme, which means that _layouts, etc is invisible for me but make a difference when built. To use a gem theme, check [Jekyll themes](https://jekyllrb.com/docs/themes/). After installing a new theme, the  `home` and `layout` in the front matter of pages must be changed to `:default`, or else it will complain.

2. Link

   Links to the content files in the markdown is commonly used, the path for the url ==can not== use `.` or `..` , one good way to link properly is to use [Liquid tags](https://jekyllrb.com/docs/liquid/tags/), such as

   ```html
   [Jekyll beginning]({{ site.baseurl }}{% link _posts/2021-08-28-Jekyll_beginning.markdown %})
   # Since liquid grammar will be transformed, better check it as raw
   ```
   
   which can work properly



 



