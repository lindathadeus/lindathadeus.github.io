---
layout: distill
title: "How to setup github pages?"
date: 2024-08-19 10:30:00 +0530
categories: blog
tags: linux
---

# How to setup github pages?

This is my first post on my new Jekyll-powered website. 

In this post, we will look at the steps to create a website using github pages.
The github pages has its limitations too. It can only serve static sites. But, for a portfolio website, this is more than enough. Blogging can also be done using the github's comments feature.

Github uses jekyll, which is a static site generator for this.

So, let us get into it

Steps

1. Create a repository like <username>.github.io and make the default branch as main
2. install jekyll, blunder
3. Follow below cli

{% highlight python %}
git clone git@github.com:lindathadeus/lindathadeus.github.io.git
sudo apt install jekyll

cd name.github.io
jekyll new .

git add .
git commit -m "hello github pages"
git push origin main
{% endhighlight %}

And, then, goto https://lindathadeus.github.io, thats it!

Hope, you could set it up too :)
Stay tuned for more!
