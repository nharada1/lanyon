---
layout: post
title: How I Made a Clean, Customized Blog with Jekyll, Poole, and Github Pages. With the Cloud.
comments: True
---

When I decided to replace my old WordPress blog, I was torn on what platform would be best. My [portfolio homepage](http://www.nateharada.com) was already hosted on Github Pages, and I liked the idea of version control and free hosting combined. WordPress was easy to use for basic blogging, but creating a site that felt personalized and not like a template was difficult for me. I settled on Jekyll with Github pages - it was free, there were [good resources](https://help.github.com/articles/using-jekyll-with-pages) available, and it was a light and customizable static site generator.

I settled on the Poole theme [Lanyon](http://lanyon.getpoole.com/) for my new blog, but I had to make some customizations to get the look I truly wanted. I removed the sidebar completely and created a page at "_includes/menu.html" to replace it. Although I liked the Lanyon design, I wanted an even more minimalist theme since I only had a few links for the navigation.

For those interested, you can find the source for my customizations on my [github page]({{ site.author.github }}), and a good tutorial for most of the setup I did on [Joshua Lande's blog](http://joshualande.com/jekyll-github-pages-poole/). 

## Developing Virtually with Amazon EC2
Supporting Windows has historically been viewed as an unfortunate but necessary evil by software developers. Historically, the hardcore open source junkies targeted only *nix systems while everyone else supported both *nix and the more popular Windows architecture. This has begun to change as Apple gains market share, due in (large) part to the iPhone's dominance in the mobile market and the fact that iOS development requires a Mac. With Macs (and thus Unix based systems) now more popular with the kids, fewer open source software maintainers are putting in the work to support Windows. The Jekyll project alone officially only supports OSX and Linux. In our case, Github pages offers an [easy way](https://help.github.com/articles/using-jekyll-with-pages) to install their entire toolchain on your local machine, but only if you're on an operating system that Jekyll supports.

As much as I love Linux, there are too many unsupported software packages for me to justify switching my machine over entirely. I could dual boot (pain in the ass), virtualize (hardware intensive), or buy a Mac (too expensive). That's where Amazon's [web services](http://aws.amazon.com/) come in to save the day. By using Amazon's EC2 compute cluster, we can access a linux machine in the cloud for almost free (in fact, it **is** free for the first year). 

To get started, go ahead and sign up for Amazon EC2 and launch a new instance.

![post-image-full](/assets/blog-jekyll-poole/launch-instance.png)

For the free tier we need to use the *micro* sized instance. If you for some reason think you want more computing power, feel free to pick another size. Remember that as long as you use an EBS storage instance you can resize your compute instance later if you need more or less power.

Once you have your new instance initialized, you can connect to it via SSH. Go to the "Instances" page and record your public DNS for your SSH client.

![post-image-full](/assets/blog-jekyll-poole/view-instance.png)

Amazon offers a guide to connecting [via PuTTy](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/putty.html) for those of you who use it. Once you're connected to your machine you can install the software packages you'll need to develop using Jekyll. First, however, you'll need to update your Ruby version or the software won't build.

{% highlight awk %}
sudo apt-get update
sudo apt-get remove ^ruby
sudo apt-get install ruby-1.9.3
sudo apt-get install build-essential git-core
gem install bundler
{% endhighlight %}

Now clone your blog's repository and create a file in that directory called "Gemfile" that contains the following:

{% highlight awk %}
source 'https://rubygems.org'
gem 'github-pages'
{% endhighlight %}

then run `bundle install` to install all of the packages that Github uses on its servers. 

From here on out you can run Jekyll on your AWS instance via `jekyll serve` and connect to it by connecting to port 4000 of the public DNS address you found earlier. Note that to do this you'll need to change the security policy of your machine to alow traffic through TCP port 4000. 

![post-image-full](/assets/blog-jekyll-poole/security.png)

Now you can do your development remotely and view changes in real time (as well as debugging information) without needing to install anything on your local machine. I use [tmux](http://tmux.sourceforge.net/) and [vim](http://www.vim.org/) for my coding. I also created a CNAME rule with my domain name provider to redirect `develop.nateharada.com` to my AWS instance so I don't need to keep entering the DNS name each time. Note that I leave my instance running 24/7, but if I stopped it the DNS name would likely change and this wouldn't work.
