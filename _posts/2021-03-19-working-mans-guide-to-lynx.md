---
layout: post
title: Lynx: A Working Man's Guide
category: software
tags: [lynx, unix]
---

# The Working Man's Guide To Lynx

* `?` view help

# customization

`/etx/lynx.cfg`

Set locations to bookmark file, jump file, enable key-bindings (vi|emacs), (white|black)list domains, cookies, and lots more.

`/etx/lynx.lss`

Modify lynx style.

# bookmarks
* `v` view bookmarks
* `a` add bookmark
  * `r` remove bookmark (bookmarks view)

# document view
* `V` visited links page
* `A` view page links
* `L` view visible links
* `d` download document
* `del` history
* `shift-g` show address of current doc
* `shift-e` show address of current link
* `=` view info about current doc
* `\` toggle source

# navigating
* `ctrl-n` move forward 2 lines
* `ctrl-p` move backward 2 lines
* `space` move to next page
* `b` move to previous page

# misc
* ':[tab]` show available commands
* `:LINE` adjust page layout
* `:TO_CLIPBOARD` copy to clipboard

# cookie-jar
* `ctrl-x` cache-jar

# prompt
* `ctrl-g` cancel current prompt

# editor
* `ctrl-x-e` open external editor

# jumpfile

Set location in lynx.cfg: `JUMPFILE:/your/path/lynx_jumps.html`

* `ctrl-j` jump file

Arguably lynx's most powerful asset. Use `%s` in a url and lynx will prompt for
input terms for each one.
Example: 

```html
<dl> 
  <dt>?<dd><a href="file::/home/username/lynx_jumps.html">This Shortcut List</a>
  <dt>c<dd><a href="https://lite.duckduckgo.com/lite?q=%s%20cppreference.com">CPP Reference</a>
  <dt>cpp<dd><a href="https://www.cplusplus.com/search.do?q=%s">CPP Manual(search)</a>
  <dt>ddg<dd><a href="https://www.duckduckgo.com/lite?q=%s">DuckDuckGo</a>
</dl>

