---
layout: post
title: Notes Archive is Live 
comments: True
---
As an electrical engineering major, computer notes don't really work. Getting math into OneNote is even worse than getting math into Word, and so for most of undergrad I stuck to paper and pencil. In my last semester I decided to try using [Markdown Notes](http://www.markdownnotes.com) to both organize notes in my machine learning class as well as practice my LaTeX. Unfortunately the website was not maintained well and after emailing the author several times with no response asking to help contribute (the bugs fixes and features I needed weren't being worked on), I decided that this year I would try something different.

I set up an instance of Hyde, a [Poole](http://www.getpoole.com) theme that runs on the Jekyll platform (the same platform that runs this blog). To separate posts into classes I used the [generate categories plugin](http://github.com/recurser/jekyll-plugins) which allows me to create a "categories" page, as well as display categories in my sidebar menu. However, Github (wisely) does not allow arbitrary code execution on their site via plugins, so I had to create a separate branch for the public site. Using instructions at the [sorry app blog](http://blog.sorryapp.com/blogging-with-jekyll/2014/01/31/using-jekyll-plugins-on-github-pages.html), I created a rake file to publish the blog for me. Now when I get to class, I just create a post in the master branch and run "rake blog:publish" to push to the server.

If you're interested in any of my notes feel free to check them out at [notes.nateharada.com](http://notes.nateharada.com).
