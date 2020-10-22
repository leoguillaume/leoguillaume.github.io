---
layout: single
title: "How create a blog in 5 minutes for free ?"
excerpt: "A tutorial to create a blog with Github Pages, Jekyll and Minimal Mistakes template"
categories:
  - web
read_time: true
author_profile: true
toc: true
share: true
comments: true
---
*In this article, I describe how I create this blog. Thanks to [Mael Fabien](https://maelfabien.github.io/) for the idea and for his great blog which served as inspiration :raised_hands:.*

# Some words of introduction...

Creating a blog, like any website, it generaly goes with writing scripts in HTML and CSS and hosting them on a web server. Here none of that, thanks to 3 tools: Github pages, Jekyll and Minimal Mistakes template. And all you need is a Github account, but first, let's talk about these tools.

* **[Github Pages](https://pages.github.com/)**

> *"Hosted directly from your GitHub repository. Just edit, push, and your changes are live."*

This is how Github Pages defines it. Github Pages is a feature of Github that allows to host a website from a Github repository, on *github_username.github.io* url. Storage space is limited but more than enough for a blog and Github Pages has two major advantages: hosting is free and works on the basis of a Github repository. The changes you push on your repository will be displayed on your site, which is really handy!

* **[Jekyll](https://jekyllrb.com/)**

Jekyll is a popular open source static site generator. It's developped on Ruby but don't worry, you won't need to know Ruby. Jekyll was developped by GitHub co-founder Tom Preston-Werner and therefore it's specially adapted to Github pages. Jekyll is very useful because is support many languages like HTML, Liquid and Markdown!

* **[Minimal Mistakes template](https://github.com/mmistakes/minimal-mistakes)**

Finaly, a very practical feature of Jekyll is the use of templates. There are a lot of templates available, some of them are free and some are paid for. Here we will use a very popular open source template: Minimale Mistake. It has the advantage of being sober, easy to use and to propose several skins.

Now, let's get to the heart of the matter!

# Step 1: the Github page

The first step is to create a new Github repository. The repository must have *github_username.github.io* as its name.

![image](https://leoguillaume.github.io/assets/images/2020-22-10-blogtutorial/screenshot-1.png){:height="60%" width="60%"}

Then import [Minimal Mistake repository](https://github.com/mmistakes/minimal-mistakes) on you new repo (copy the url and add .git at the end).

![image](https://leoguillaume.github.io/assets/images/2020-22-10-blogtutorial/screenshot-2.png)

:bulb: Remember to change the default branch to the master branch.

![image](https://leoguillaume.github.io/assets/images/2020-22-10-blogtutorial/screenshot-3.png){:height="50%" width="50%"}

Now you can load your blog on any search engine (it's can take few minutes). Congratulations, you have just put your blog online :tada:!

![image](https://leoguillaume.github.io/assets/images/2020-22-10-blogtutorial/screenshot-4.png)

Ok cool but there's nothing on it yet. Now we're going to edit some files to give it a more personal touch.

# Step 2: Configurations

First of all, we need to clone the repo in local (copy the url and add .git at the end) and to delete useless files.

```console
git clone https://<url>.git
rm screenshot-layouts.png screenshot.png
rm -rf test docs
```

`test` and `docs` directory are documentation folders, if they are useless here, feel free to refer to them in the Minimal Mistakes repo. You will find all the features offered by the template.

:bulb: Remember to change the README.md file too!

Now open your favorite text editor to modify `_config.yml`. The file is the core of the blog, it gathers many informations about your blog. It's very clear because the signification of each tag is described.

## The blog header

You'll find blog header configurations in `Site Settings` block in `_config.yml` file.

*Example for this blog:*
```yml
minimal_mistakes_skin    : "default" # "air", "aqua", "contrast", "dark", "dirt", "neon", "mint", "plum", "sunrise"

# Site Settings
locale                   : "en-US"
title                    : "Léo's Data Science Blog"
title_separator          : "-"
subtitle                 : # site tagline that appears below site title in masthead
name                     : "Léo Guillaume"
description              : "Data scientist"
url                      : "https://leoguillaume.github.io" # the base hostname & protocol for your site e.g. "https://mmistakes.github.io"
baseurl                  : # the subpath of your site, e.g. "/blog"
repository               : "leoguillaume/leoguillaume.github.io" # GitHub username/repo-name e.g. "mmistakes/minimal-mistakes"
teaser                   : # path of fallback teaser image, e.g. "/assets/images/500x300.png"
logo                     : "/assets/images/logo/logo.png" # path of logo image to display in the masthead, e.g. "/assets/images/88x88.png"
words_per_minute         : 150
```

:bulb: Remember to store all assets (images, logos, pdf, videos, etc.) in the `assets` folder. You can create sub-folders by file type to better manage your assets.

## Author profile

You'll find author profile configurations in `Site Author` block in `_config.yml`. Icons here are provide by [Font Awesome](https://fontawesome.com/), feel free to explore their website to find the class name of the logo to any service.

*Example for this blog:*
```yml
# Site Author
author:
  name             : "Léo Guillaume"
  avatar           : "/assets/images/avatar.jpg" # path of avatar image, e.g. "/assets/images/bio-photo.jpg"
  bio              : "Data scientist"
  location         : "Paris, France"
  email            : "leoguillaume1@gmail.com"
  links:
    - label: "Email"
      icon: "fas fa-fw fa-envelope-square"
      url: "mailto:leoguillaume1@gmail.com"
    - label: "Website"
      icon: "fas fa-fw fa-link"
      url: "https://leoguillaume.github.io"
    - label: "Twitter"
      icon: "fab fa-fw fa-twitter-square"
      # url: "https://twitter.com/"
    - label: "Facebook"
      icon: "fab fa-fw fa-facebook-square"
      # url: "https://facebook.com/"
    - label: "GitHub"
      icon: "fab fa-fw fa-github"
      url: &githubUrl 'https://github.com/leoguillaume'
    - label: 'LinkedIn'
      icon: 'fab fa-fw fa-linkedin'
      url: &linkedinUrl 'https://linkedin.com/in/léo-guillaume-578bb9141/'
```

## Blog footer

You'll find blog footer configurations in `Site Footer` block in `_config.yml`.

*Example for this blog:*
```yml
# Site Footer
footer:
  links:
    - label: 'LinkedIn'
      icon: 'fab fa-fw fa-linkedin'
      url: *linkedinUrl
    - label: 'GitHub'
      icon: 'fab fa-fw fa-github'
      url: *githubUrl
```

The last change in `_config.yml` file is the comments account but we'll see about that latter.

You can save the modifications and push them on Github :rocket:.

# Step 3: The home page
# Step 4: Posts
# Step 5: Blog structure
