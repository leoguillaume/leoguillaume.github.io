---
layout: single
title: "How create a blog in 5 minutes for free ?"
excerpt: "A tutorial to create a blog with Github page, Jekyll and "
categories:
  - web
read_time: true
author_profile: true
toc: true
share: true
comments: true
---
*In this article, I describe how I create this blog. Thanks to [Mael Fabien](https://maelfabien.github.io/) for the idea and for his great blog which served as inspiration :raised_hands:.*

**How did I create this blog in 5 min and for free?**

Creating a blog, like any website, it generaly goes with writing scripts in HTML and CSS and hosting them on a web server. Here none of that, thanks to 3 tools: Github pages, Jekyll and Minimal Mistakes theme. And all you need is a Github account, but first, let's talk about these tools.

* **[Github Pages](https://pages.github.com/)**
"Hosted directly from your GitHub repository. Just edit, push, and your changes are live." this is how Github Pages defines it. Github Pages is a feature of Github that allows to host a website from a Github repository, on *<github_username>.github.io* url. Storage space is limited but more than enough for a blog and Github Pages has two major advantages: hosting is free and works on the basis of a Github repository. The changes you push on your repository will be displayed on your site, which is really handy!

* **[Jekyll](https://jekyllrb.com/)**

Jekyll is a popular open source static site generator. It's developped on Ruby but don't worry, you won't need to know Ruby. Jekyll was developped by GitHub co-founder Tom Preston-Werner and therefore it's specially adapted to Github pages. Jekyll is very useful because is support many languages like HTML, Liquid and Markdown!

* **[Minimal Mistakes theme](https://github.com/mmistakes/minimal-mistakes)**

Finaly, a very practical feature of Jekyll is the use of templates. There are a lot of templates available, some of them are free and some are paid for. Here we will use a very popular open source template: Minimale Mistake. It has the advantage of being sober, easy to use and to propose several skins.

Now, let's get to the heart of the matter!

# Step 1: the Github page

The first step is to create a new Github repository. The repository must be name with *github_username.github.io*
![image](https://leoguillaume.github.io/assets/images/2020-22-10-blogtutorial/screenshot-1.png)
Then import [Minimal Mistake repository](https://github.com/mmistakes/minimal-mistakes) on you new repo and change the default branch to the master branch.
![image]()
![image]()

New clone the repo in local (copy the url and add .git at the end) and delete useless files.

```console
git clone https://... repo_rul.git
rm screenshot-layouts.png screenshot.png
rm -rf test docs
```
Think to change the REAMED.md file too!
