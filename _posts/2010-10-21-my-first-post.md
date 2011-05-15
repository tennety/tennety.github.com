---
title: My First Post with Jekyll
author: Chandu Tennety
layout: post
excerpt: |-
  All the cool kids were doing it, so I tried it too. I moved from Wordpress to "Jekyll":http://jekyllrb.com. It sounded so perfect: no cluttered UI, no databases to maintain, "Git":http://git-scm.com for version control, and my trusty "text editor":http://www.vim.org to write posts with. What could _possibly_ go wrong? And since you are reading this, I was successful. Eventually.
---

It all started as a bug in my head when I was trying to educate myself on Rack and Sinatra. I saw mention of [Toto](http://cloudhead.io/toto) and Jekyll, and mused taking the dive for a while, but hesitated till the awesomely cool [Adam McCrea](http://adamlogic.com) gave a talk about Jekyll at our [Columbus Ruby Brigade](http://columbusrb.com). As with anything he gives a talk about, it all sounded perfectly clear and straightforward. Just write, he seemed to say, let Ruby do the rest. Of course, I thought, I'll have it up by tonight! It was a little harder than that, but rewarding nonetheless.

The easiest version of the process, roughly, was this:

  1. Use [Github pages](http://pages.github.com) for hosting. Here's some reasons why:
      * Tom Preston-Werner wrote Jekyll, and Github groks it
      * Deploying is a cinch, just create and push to your repo and your pages are automagically updated!
      * There are plenty of other Jekyll-Github [sites](http://github.com/mojombo/jekyll/wiki/Sites) with open source for inspiration
  1. Migrate your posts from your previous blogging engine using Jekyll's adapters
  1. Include comments using Disqus 
  1. Organize content to your heart's content using Liquid

That was pretty much it. I followed the process, and here I am. Of course, there were some setbacks, and I've tried to present them as honestly as I could in the following sections.

### I'm not a Web Developer.

You must be doing a facepalm about now. Why on earth would I put myself through this if I'm not a web developer? Why couldn't I ensconce myself in the impersonal embrace of a CMS? The answer, of course, is that I did. I went from Blogspot to Blogger to self-hosted Wordpress. But each time I found myself trying to tweak the system, move things around. And each time I hit a wall of PHP that I just could not brute force my way through. I was less like a bull in a china shop, and more like a toddler with sphaghetti. Poked my eyes out a few times, and there was sauce everywhere.

Then I found Ruby, Vim and Git. And I was in love. I started looking for ways to use Ruby for blogging. Rails still seemed like overkill, though. Right about then, Jekyll came on the radar, as I mentioned earlier in the post. So fork in hand, I dove in.

I'm still editing reams of HTML and CSS, and it shows that it's far from perfect. Which leads me to my next issue.

### Markdown? Textile? Liquid?

It took me a little while to get the hang of [Markdown](http://daringfireball.net/projects/markdown/), I'm still trying to understand [Textile](http://www.textism.com/tools/textile/). But when it comes to real HTML-fu, [HAML](http://haml-lang.com/) is my favorite. However, Jekyll has no support for HAML out of the box. Yes, there are [forks](https://github.com/henrik/jekyll) that incorporate HAML, but does Github Pages support it? I don't believe it does. 

So when I started creating my landing and contact pages, I had to rely on good old HTML and CSS, since neither Markdown nor Textile (which are both meant primarily for HTML document creation) could help with page layouts.

But [Liquid](http://www.liquidmarkup.org/) was a different story. It was beautifully powerful, with its filters and tags, and Jekyll's own extensions for it. <strike>There were still some things missing, however. For instance, good post excerpting. If I want to truncate my posts to only a few sentences or paragraphs, Liquid does not have a filter for it; I can only truncate to a number of words. Liquid allows me to manipulate post excerpts, but Jekyll has no concept of an excerpt. So I'm stuck with post previews that end mid-sentence [...]</strike> 

**Update:** Search and ye shall receive. [Kevin Marsh](http://kevinmarsh.com/articles/2009/02/12/jekyll.html) tells us exactly how to use excerpts in Jekyll. I was sure that if it could be done, it would be through the metadata, I just didn't have the YAML skillz to do it. 

#### Couple of gotchas: 

  1. Since that post, Jekyll was updated with a Liquid filter to textilize excerpts, but it doesn't seem to have one for Markdown. So if you're primarily writing in Markdown, you'll still have to format your excerpt in Textile.
  1. This may be a no duh, but still worth mentioning: Inside your index.html where you're putting your newly created post excerpts, you can refer to the post variable like this: <div class="inline vim_block">{{"{{ post.excerpt | textilize " }}}}</div> However, if you're trying to stay DRY and want to call the same filter in your post itself, you'll have to do this: <div class="inline vim_block">{{ "{{ page.excerpt | textilize " }}}}</div>

  1. By the way, do yourself a favor and _never_ try to display Liquid code inside a Liquid template. If you must, [here's](http://tesoriere.com/2010/08/25/liquid-code-in-a-liquid-template-with-jekyll/) a resource that'll help.

### Syntax Highlighting - Vim to the Rescue!

Jekyll supports [Pygments](http://pygments.org/), a Python-based syntax highlighter that supports arguably every language out there. But I don't know Python. Another facepalm moment there.

The redoubtable Vim provides a way out here (albeit a little clunky). With its ToHTML feature, Vim lets me export any code block to HTML, with the current color scheme included. With a few [handy changes](http://techspeak.plainlystated.com/2009/08/vim-tohtml-customization.html), it gives me a completely workable solution to display code in my posts that looks almost exactly how it does in my editor. Don't believe me? See for yourself:

<div class="vim_block"><span class="PreProc">class</span>&nbsp;<span class="Type">OuterElement</span>&nbsp;&lt; <span class="Type">ActiveRecord</span>::<span class="Type">Base</span><br />
&nbsp;&nbsp;<span class="Constant">has_many</span>&nbsp;<span class="Constant">:inner_elements</span><br />
<span class="PreProc">end</span><br />
</div>

If that feels like too much work, there's always [Gist](http://gist.github.com) or [Pastie](http://pastie.org).

### Conclusion (and a Confession)

Yes, I confess I downloaded a [free CSS template](http://www.freecsstemplates.org/preview/perfectblemish/) to get started. I've customized it considerably, and I must say that though I was writing HTML and CSS, it was **great** to have the freedom to do whatever the hell I wanted to with it, instead of having to do it through a crappy interface. Learning curves aside (hey, I went from Eclipse to Vim, so I know learning curves), Jekyll does very well with a small set of tools. Any limitations are largely self-imposed.

Additionally, this is exactly the intro to web development I know I need. It's forcing me to get my lazy butt into building a site brick by brick, while making it easy to do the one task I would rather not be doing in code -- writing. And that is why I chose to put the result out there as-is, warts and all, for all to see. I hope I can make it grow into something beautiful. 
