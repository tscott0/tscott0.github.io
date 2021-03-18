---
title: "Hosting a Hugo site with GitHub Pages"
date: 2021-03-18T13:26:06Z
draft: false
---

How to build a simple site with Hugo and deploy it to GitHub Pages automatically<!--more-->

## So what is Hugo?

Hugo is a tool to generate static sites. It consists of a CLI that can
- create the scaffolding for a new site;
- add new content; and
- spin up a local, hot-reloading webserver.

Like [Jekyll](https://en.wikipedia.org/wiki/Jekyll_(software)) before it, Hugo supports a [vast number of themes](https://themes.gohugo.io/). Sites output by Hugo are largely static, meaning they primarly consist of HTML and CSS.

Adding new content, like this very post, is as simple as creating a markdown file. These files can be created by hand but I find it easier to use the `hugo new` subcommand, as shown in the [quick start guide](https://gohugo.io/getting-started/quick-start/).

```markdown
---
title: "Hosting a Hugo site with GitHub Pages"
date: 2021-03-18T13:26:06Z
draft: true
---

How to build a simple site with Hugo and deploy it to GitHub Pages
<!--more-->
...
```

## GitHub Pages

GitHub provides [Pages](https://pages.github.com/) as a convenient way to serve static pages from a Git repository. It supports custom URLs but if you don't have your own domain, there is a free subdomain for every user available at  `<username>.github.io` - neat! There are [some limitations](https://docs.github.com/en/github/working-with-github-pages/about-github-pages#guidelines-for-using-github-pages), but the usage limits are quite reasonable.

## GitHub Actions

Actions provide a simple way to automate CI/CD tasks in the form of workflows. I created [a simple workflow](https://github.com/tscott0/tscott0.github.io/blob/main/.github/workflows/gh-pages.yml) to generate this site on every commit by following [this guide on gohugo.io](https://gohugo.io/hosting-and-deployment/hosting-on-github/). 


Deployments to GitHub Pages are now totally automated. The workflow will
- clone the repo;
- download latest version of Hugo;
- `hugo --minify` to generate the site; and
- push the newly generated site to the `gh-pages` branch of the same repo.

## My workflow

When I have an idea for a new post, these are the steps I follow.

1. Start a local server for previewing changes with `hugo server -D`
1. Create a new draft post with `hugo new posts/your-post.md`
1. Write some interesting content (the hard bit). Usually I'll use VSCode or vim to do the editing.
1. Review the new post.
1. Update the header to set `draft: false` when finished
1. Commit and push changes to `main`
1. GitHub Actions Workflow runs automatically

GitHub is looking for changes on the `gh-pages` branch of the `tscott0.github.io` repository. In my experience the site updates almost instantaneously after the workflow succeeds. Usually I'll manually confirm that the site is updated

## Moving on

I'm a big fan of GitHub Actions and use it regularly at work. I'm a big fan of "light" webpages to; ones that render quickly on mobile and on desktop. I find it shocking that the average webpage is more than 2MB these days! 🤦‍♂️ I'm hoping that Hugo will help keep these pages nice and small.

One of my goals is to improve my technical writing skills. As a software engineer I'm always playing with technology. I suppose it's about time I started documenting some of it. Using Hugo with GitHub Actions make it so easy that I've really got no excuses any more.