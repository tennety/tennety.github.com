---
title: My First Post with Jekyll
author: Chandu Tennety
layout: post
---

All the cool kids were doing it, so I tried it too. I moved from Wordpress to [Jekyll](http://jekyllrb.com). It sounded so perfect: no cluttered UI, no databases to maintain, [Git](http://git-scm.com) for version control, and my trusty [text editor](http://www.vim.org) to write posts with. What could _possibly_ go wrong?

And since you are reading this, I was successful. Eventually.

It all started as a bug in my head when I was trying to educate myself on Rack and Sinatra. I saw mention of [Toto](http://cloudhead.io/toto) and Jekyll, and mused taking the dive for a while, but hesitated till the awesomely cool [Adam McCrea](http://twitter.com/adamlogic) gave a talk about Jekyll at our [Columbus Ruby Brigade](http://columbusrb.com). As with anything he gives a talk about, it all sounded perfectly clear and straightforward. Just write, he seemed to say, let Ruby do the rest. Of course, I thought, I'll have it up by tonight! It was a little harder than that, but rewarding nonetheless.

The easiest version of the process, roughly, was this:

  1. Use [Github pages](http://pages.github.com) for hosting. Here's why:
      * Tom Preston-Werner wrote Jekyll, and Github groks it
      * Deploying is a cinch, just create and push to your repo and your pages are automagically updated!
      * There are plenty of other Jekyll-Github sites with open source for inspiration
  1. Migrate your posts from your previous blogging engine using Jekyll's adapters
  1. Include comments using Disqus 
