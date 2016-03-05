---
layout: post
title: Setting up my blog on Github
categories:
- blog
tags:
- blog
---

Github allows you to create a website for your account.  By creating a repo named '*username*.github.io', github will serve up the content in the repo at http://username.github.io.  You can create your own static content, but Github also integrates [Jekyll](http://jekyllrb.com) to create content from markdown files.


##Local Jekyll
You can set up a Github Pages site directly from the Github site, and manage your blog configuration and create your blog posts from there.  However, I chose to install Jekyll on my local system so that I can test out configuration changes and view new posts before they go live to the world.

Github provides the ['github-pages' ruby gem](https://github.com/github/pages-gem) that will replicate the Github Pages environment locally.  To make this work on my Mac (OS X 10.11), I needed:

- Python (python 2.7 comes with OS X)
- Ruby (again, OS X comes with ruby 2.0 and gem 2.0)
- Xcode command line tools, for building new gems.  I didn't have the tools installed, so I installed them by typing:

~~~ shell
$ xcode-select --install
~~~

Then to install github-pages I ran:

~~~ shell
$ gem install --user-install github-pages
~~~

I used "\--user-install" to install the gems in my home directory so that I didn't mess with the system's ruby installation.  Because of that, I had to add the gem executable path to my $PATH; I ran this command, and also added it to my .bash_profile.

~~~ shell
export PATH=$PATH:~/.gem/ruby/2.0.0/bin
~~~


##Choosing and testing the blog theme
To make your blog pleasant to look at, there are lots of free pre-made Jekyll themes available.  A few theme sites that I looked at were:

<https://github.com/jekyll/jekyll/wiki/Themes>\\
<http://jekyllthemes.io>\\
<http://jekyllthemes.org>\\
<http://themes.jekyllrc.org>

I decided on the [lagom theme](https://github.com/swanson/lagom) by Matt Swanson because I like its uncomplicated look and the way that its landing page is just a list of blog posts in reverse chronological order.  Easy to read, nothing fancy -- perfect.

I created a new repo on github named "jwoest.github.io".  Then I cloned the logam theme repo to my local system and set my new github repo as a remote:

~~~ shell
$ git clone https://github.com/swanson/lagom jwoest.github.io
$ cd jwoest.github.io
$ git remote remove origin
$ git remote add origin https://github.com/jwoest/jwoest.github.io
~~~

Now I could test that Jekyll would correctly serve up the blog before I made any modifications, but I did have to make one small change first.  Github Pages only supports "rouge" for syntax highlighting, but the lagom theme comes configured for "pygments".  I edited the _config.yml file and changed the highlighter setting:

~~~ yaml
highlighter: rouge
~~~

Then I started up Jekyll to serve the site from my local system:

~~~ shell
$ jekyll serve
~~~

Pointing my browser at http://localhost:4000 showed the default site for the logam theme.


##Making it mine
Customizing the blog theme as my own meant modifying several files.

- logo.png
  - Replaced with a new image of my smiling face
- _config.yml
  - Changed the 'url' setting to "http://jwoest.github.io".  This is used by the RSS feed, which is enabled by default.
- _data/theme.yml
  - Set "highlight_color" to a darker shade of blue.  This is the color used for link text and the bar across the top of the page.
  - Set my social media account names, used for the links in the sidebar
  - Set my name for the "Hi I'm NAME" sidebar text
  - Disable the disclaimer text in the footer
- _includes/footer.html
  - minor formatting changes to footer text
- _includes/sidebar.html
  - Customize the bio text
- _layouts/post.html:
  - Change text at the bottom of blog posts reading "Related posts" to "Recent posts".  The 'site.related_posts' variable by default just contains the ten most recent posts whether they are related to the current post or not.
- _posts/
  - Remove the two sample posts

Then I restarted 'jekyll serve' and confirmed my changes by viewing the local website.


##Going live
Once I was satisfied with the way my site looked, I commited the changes and pushed them up to github

~~~ shell
$ git add .
$ git commit
$ git push origin master
~~~

Pointing my browser to <http://jwoest.github.io> showed me my new website, live on the Internet!

Now I had a blog *site*, but no actual blog *posts*.  My next post will cover how I created my first blog post and inflicted it upon the world.


