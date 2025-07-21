---
title: "Using Hugo to generate the static site"
date: 2022-07-13T23:40:00+01:00
draft: true
toc: false
images:
tags: 
  - Review
  - How-to
---

Based on my experience, starting to use [Hugo](https://gohugo.io/) is quite accessible. See [quick-start](https://gohugo.io/getting-started/quick-start/).

There are plenty of themes to part from, and they are simple to configure to your liking (just following the instructions in each Theme).
For those already used to writing Markdown documents, using Hugo is straightforward.
It gives a clean façade to those parsed documents and lets you navigate and cross-reference them.

## As an example: Using Hermit theme

The default theme style matched the aesthetic I was looking for, so my configurations were more data related in this case.

I started with the indicated configuration in the README.md of Hermit's Github repository and adapted it as follows:

``` 
title = '/ˈtɛknɪkəl ˈraɪtɪŋ/'
theme = 'hermit'

[author]
  name = "Luis J. González"

[taxonomies]
  tag = "tags"

[params]
  dateform        = "Jan 2, 2006"
  dateformShort   = "Jan 2"
  dateformNum     = "2006-01-02"
  dateformNumTime = "2006-01-02 15:04 -0700"

  themeColor = "#494f5c"
  homeSubtitle = "Notes for myself and whoever may find them useful"
  footerCopyright = ' &#183; <a href="https://creativecommons.org/licenses/by-nc/4.0/" target="_blank" rel="noopener">CC BY-NC 4.0</a>'

  relatedPosts = false
  code_copy_button = true

  [[params.social]]
    name = "github"
    url = "https://github.com/luis-javier-gonzalez-alonso"

  [[params.social]]
    name = "linkedin"
    url = "https://www.linkedin.com/in/luis-javier-gonz%C3%A1lez-22a201189/"

[menu]
  [[menu.main]]
    name = "Posts"
    url = "posts/"
```

After these basic configurations, the site was ready to use.
