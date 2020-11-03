---
layout: single
title: "How build a blog in few minutes for free ?"
excerpt: "A tutorial to build a blog with Github Pages, Jekyll and Minimal Mistakes template"
header:
    teaser: https://leoguillaume.github.io/assets/images/2020-10-22-blogtutorial/teaser.jpg
categories:
  - web
read_time: true
author_profile: true
toc: true
tags:
  - github
  - jekyll
share: true
comments: true
---
*In this article, I describe how I build this blog. Thanks to [Mael Fabien](https://maelfabien.github.io/) for the idea and for his great blog which served as inspiration :raised_hands:.*

# Some words of introduction...

Creating a blog, like any website, it generaly goes with writing scripts in HTML and CSS and hosting them on a web server. Here none of that, thanks to 3 tools: Github pages, Jekyll and Minimal Mistakes template. And all you need is a Github account, but first, let's talk about these tools.

* **[Github Pages](https://pages.github.com/)**

> *"Hosted directly from your GitHub repository. Just edit, push, and your changes are live."*

Github Pages is a Github feature allowing users to host a website from a Github repository, with *github_username.github.io* url. Storage space is more than enough for a blog and Github Pages has two major advantages: hosting is free and works as a Github repository. The changes you push on your repository will be displayed on your website, which is really handy!

* **[Jekyll](https://jekyllrb.com/)**

Jekyll is a popular open source static website generator. It's Ruby based but don't worry, you won't need to know Ruby. Jekyll was developed by GitHub co-founder Tom Preston-Werner and therefore it's specially adapted to Github pages. Jekyll is very useful because it has a responsive design and it supports many languages as HTML, Liquid and Markdown for your posts!

* **[Minimal Mistakes template](https://github.com/mmistakes/minimal-mistakes)**

Finally, a very practical feature of Jekyll is the use of templates. There are a lot of templates available, free or not. Here we'll use a very popular open source template: Minimale Mistake. It has the advantage of being sober, user-friendly and to propose several skins.

Now, let's get to the heart of the matter!

# Step 1: the Github page

The first step is to create a new Github repository. The repository must have *github_username.github.io* as its name.

![image](https://leoguillaume.github.io/assets/images/2020-10-22-blogtutorial/screenshot-1.png){:height="60%" width="60%"}

Then import [Minimal Mistake repository](https://github.com/mmistakes/minimal-mistakes) on you new repo (copy the url and add .git at the end).

![image](https://leoguillaume.github.io/assets/images/2020-10-22-blogtutorial/screenshot-2.png)

:bulb: Remember to change the default branch to the master branch.

![image](https://leoguillaume.github.io/assets/images/2020-10-22-blogtutorial/screenshot-3.png){:height="50%" width="50%"}

Now you can load your blog on any web browser (it can take few minutes). Congratulations, you have just put your blog online :tada:!

![image](https://leoguillaume.github.io/assets/images/2020-10-22-blogtutorial/screenshot-4.png)

Great, but there's nothing on it yet. Now we're going to edit some files to give it a more personal touch.

# Step 2: Configurations

First of all, we need to clone the repo in local (copy the url and add .git at the end) and to delete useless files.

```console
git clone https://<url>.git
rm screenshot-layouts.png screenshot.png
rm -rf test docs
```

`test` and `docs` directory are documentation folders, if they are useless here, feel free to refer to them in the Minimal Mistakes repo. You'll find all the features offered by the template.

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

You'll find author profile configurations in `Site Author` block in `_config.yml`. Icons here are provided by [Font Awesome](https://fontawesome.com/), feel free to explore their website to find the class name of the logo to any service.

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

The home page is contained in the `index.html` file. Open it and write a welcome message :pencil2:.

```html
---
layout: home
author_profile: true
---

<b>Welcome to my blog!</b>
```

You can see at the start of the file a front matter block with `layout` and `author_profile`. This block is an essential part of Jekyll, it defines the global variables for the page or the post. We'll see this more in detail in the next section dealing with posts.

# Step 4: Posts

*[See the documentation](https://jekyllrb.com/docs/posts/)*

Now it's time to write your first post :raised_hands:! In Jekyll, you write blog posts as text files (HTML or Markdown) and Jekyll provides everything you need to turn it into a blog. The first step is to create a `_posts` directory in the root of the project directory. This folder will storage your post files.

```console
mkdir _posts
```

To create a post, add a file to your `_posts` directory with the following format: `YEAR-MONTH-DAY-title.MARKUP`. Where `YEAR` is a four-digit number, `MONTH` and `DAY` are both two-digit numbers, and MARKUP is the file extension representing the format used in the file (.html or .md).

For example to create a new post today:
```console
touch _posts/2020-22-10-myfirstpost.md
```

At the head of your file text, there must be a front matter block like this:

```yml
---
layout: single
title: "My first post"
excerpt: "Test post"
categories:
    - web
header:
      teaser: https://leoguillaume.github.io/assets/images/2020-10-22-blogtutorial/teaser.jpeg
read_time: true
author_profile: true
toc: true
share: true
comments: true
---
```

`layout` is the template of your page, for post `single` layout is the most appropriate. *[See all layouts](https://mmistakes.github.io/minimal-mistakes/docs/layouts/)*
`author_profile` display the side bar with author informations (defined in the config file).
`toc` display the table of contents.
`categories`, we'll see in the next section the interest of categorising the posts.
`comments` display a comment box at the end of your post. To activate this feature you must modify the `Site Settings` block in the `_config.yml` file and choice a comment service. Here I choose [Disqus](https://disqus.com/) because it's free, popular and user-frendly. To get the shortname Disqus, you must configure your website on Disqus and go to the admin page.

```yml
comments:
  provider               : "disqus" # false (default), "disqus", "discourse", "facebook", "staticman", "staticman_v2", "utterances", "custom"
  disqus:
    shortname            : 'https-leoguillaume-github-io' # https://help.disqus.com/customer/portal/articles/466208-what-s-a-shortname-
  discourse:
    server               : # https://meta.discourse.org/t/embedding-discourse-comments-via-javascript/31963 , e.g.: meta.discourse.org
  facebook:
    # https://developers.facebook.com/docs/plugins/comments
    appid                :
    num_posts            : # 5 (default)
    colorscheme          : # "light" (default), "dark"
  utterances:
    theme                : # "github-light" (default), "github-dark"
    issue_term           : # "pathname" (default)
  staticman:
    branch               : # "master"
    endpoint             : # "https://{your Staticman v3 API}/v3/entry/github/"

```

Now all you have to do is write your post. You'll see all your posts in the home page, under your welcome message, in a "Recent posts" box.

:bulb: Remember all images and ressources you want to include must be save in the `assets` folder in the root of your project directory.

# Step 5: Blog structure

Great we have a homepage with a welcome message and a list of your posts, now we have to build the rest of the blog structure. If you load your site on a web browser you'll see the different tabs in the header of your blog. For the moment there is only one by default, "Quick-Start Guide". We will see how to create different pages to present your posts by category, your portfolio and your resume.  

## Navigation

[See documentation](https://mmistakes.github.io/minimal-mistakes/docs/navigation/)

Organising the structure of your blog is very simple with Jekyll. In the `_data` directory, you'll find a `navigation.yml` file that will modifies the navigation tabs.

You'll create three tabs:
- a "blog" tab with posts by categories
- a "portfolio" tab with a project gallery
- a "curriculum" tab with a resume

### The blog tab

Go in your first post and click on the *web* category below your post.

![image](https://leoguillaume.github.io/assets/images/2020-10-22-blogtutorial/screenshot-5.png)

This will take you to the following url:

![image](https://leoguillaume.github.io/assets/images/2020-10-22-blogtutorial/screenshot-6.png)

You will therefore return the blog tab to the *categories* page which does not yet exist.

You'll modify the `navigation.yml` file like this:
```yml
main:
  - title: 'Blog'
    url: /categories/
```

### The portfolio tab

In the next section we'll create a *projects* page to display the gallery of your project.

```yml
main:
  - title: 'Blog'
    url: /categories/
  - title: 'Portfolio'
    url: /projects/
```

### The curriculum tab

The *curriculum* tab leads directly to the resume in PDF, storage in the assets folder.

```yml
main:
  - title: 'Blog'
    url: /categories/
  - title: 'Portfolio'
    url: /projects/
  - title: 'Curriculum'
    url: /assets/pdf/resume2020.pdf
```

## Pages

You have created navigation tabs which leads to urls, now you have to build pages of these urls. The way of adding a page is to add an HTLM or Markdown files in the `_pages` directory.

To create a index page which leads posts by category, you have to create a Markdown file with `categories` layout, like this:

```yml
---
layout: categories
title: "Posts by category"
permalink: /categories/
author_profile: true
---
```

To create the portfolio page, you can copy the code below which generate a gallery of posts in the *project* category.

```
layout: archive
title: "Portfolio and projects"
permalink: /projects/
author_profile: true
---
<div class="grid__wrapper">
    {% for post in site.posts %}
        {% if post.categories contains 'project' %}
            {% include archive-single.html type="grid" %}
        {% endif %}
    {% endfor %}
</div>
```

Save the modifications and push them on Github :rocket:! Well done, you have now everything you need to create your blog.

The reader must be warned that this document is not exhaustive and that Jekyll and Minimal Mistakes offer many other possibilities. All of them are easily modifiable and there are a lot of features to be discovered. Feel free to explore the documentations to explore all the possibilities and make your blog more personal:
- [Jekyll documentation](https://jekyllrb.com/docs/)
- [Minimale Mistakes documentations](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/)

Ps: feel free to fork also the [repo of this blog](https://github.com/leoguillaume/leoguillaume.github.io) :grin:.
