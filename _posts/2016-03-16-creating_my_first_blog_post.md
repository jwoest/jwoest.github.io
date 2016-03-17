---
layout: post
title: Creating my first blog post
categories:
- blog
tags:
- blog
---
My new blog looked pretty bare with no content; here's how I created that first post.


## File locations: posts and drafts
When Jekyll is run and builds a site, it looks in two subdirectories for blog posts:  

*_posts*  
'Live' blog posts, published on your site.  Jekyll expects files here to be in the form of *YYYY_MM_DD_post_name.md*.  (The '.md' extension is for 'markdown'; more on that below.)  When published, Jekyll will serve the posts up at URLs of the form http://user.github.io/YYYY/MM/DD/post_name.html.

*_drafts*  
Blog posts that you are working on but don't want to go live on your site.  File names are of the form *post_name.md*.  When you run your local Jekyll server with the "\--drafts" flag, it will publish the draft posts with URLs of the form http://localhost:4000/YYYY/MM/DD/post_name.html, where the date on the post is the curent date.

So to begin working on my [first blog post]({% post_url 2016-02-25-blog_go %}), I created *_drafts/blog_go.md*, and then launched Jekyll:

~~~ shell
$ jekyll serve --drafts
~~~

When you run "jekyll serve" (with or without '\--drafts'), it will stay up and running.  If you make a change to the contents of your blog (your local copy), jekyll will detect the change and rebuild your blog contents so that you can preview them at http://localhost:4000.

## Front matter
At the top of the Jekyll blog posts is "front matter", some YAML metadata that tells Jekyll how to format your post.  For my first blog post, the front matter looks like this:

~~~ yaml
---
layout: post
title: Blog go!
categories:
- blog
tags:
- blog
---
~~~

The front matter block starts and ends with "\-\--".  The fields I used for my first post were:

~~~ yaml
layout: post
~~~
- Points Jekyll to the HTML template in the _layouts sibdirectory named "post.html" for formatting.  By using this tag on all blog posts, every post will have the same look and feel.

~~~ yaml
title: Blog go!
~~~
- Sets the title at the top of the blog post.  The layout file will include this by referencing the "page.title" tag.

~~~ yaml
categories:
- blog
~~~
- Setting a category for a post causes Jekyll to publish it under a subdirectory.  By setting a single category of "blog", my post will get published as  

  ~~~
  /blog/YYYY/MM/DD/post_name.html  
  ~~~
  instead of just  

  ~~~
  /YYYY/MM/DD/post_name.html 
  ~~~
  Setting more than one category will cause extra subdirs to be added as well; categories of "blog" and "test" will create the URL as "/blog/test/YYYY/...".

~~~ yaml
tags:
- blog
~~~
- Sets a tag for the page (this is a blog post about my blog!).  May be useful in the future for creating lists of posts about similar topics.

## Markdown
After the front matter, a blog post is written in markdown.  Jekyll supports a variety of markdown formats, but Github Pages defaults to [kramdown](http://kramdown.gettalong.org) and in fact will soon support *only* kramdown.

My first blog post was actually all just text with no  markdown tags (the shame!) but here are some examples of kramdown formatting that I've used in my other blog posts:

- H2 header for section headings

~~~
## Heading
~~~

- *Italics* and **bold**

~~~
*Italics*
**Bold**
~~~

- Bullet-point lists

~~~
- item 1
  - subitem 1
- item 2
- item 3
~~~

- Links

~~~
[Google search](https://www.google.com)
~~~
This creates a link like this: [Google search](https://www.google.com)

- Syntax highlighting.  Github pages uses the [rouge](http://rouge.jneen.net) for code highlighting.  Rouge provides support for dozens of languages.  As an example, here's how the "front matter" text block example towards the top of this post was highlighted using the 'yaml' tag:

~~~~
~~~ yaml
---
layout: post
title: Blog go!
categories:
- blog
tags:
- blog
---
~~~
~~~~


## Previewing and publishing
Once I was done writing my blog post, I moved it from the draft location:

~~~
_drafts/blog_go.md
~~~

to it's 'live' location:

~~~
_posts/2016-02-25-blog_go.md
~~~

Then I restarted Jekyll without the '\--drafts' flag to preview the post as it would appear once it went live on Github Pages.  Satisifed with my work, I committed the change to the local git repo and then pushed it up to Github.  Once it was there, I could see it on my blog on Github Pages.  Finally, some content for my blog!

