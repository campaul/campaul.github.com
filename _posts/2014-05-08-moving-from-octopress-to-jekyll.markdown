---
layout: post
title: "Moving from Octopress to Jekyll"
date: 2014-05-08
comments: true
categories: []
---
Octopress is complicated and confusing. You start by cloning an existing project to work out of. If you use GitHub Pages, you keep your source files in an orphan branch and build into master. If you ever need to update, you pull from Octopress and deal with the merge conflicts with any tweaks you've made to the theme. There are lots of bells and whistles, but they come at a cost. I wanted to simplify.

Luckily Octopress is built on Jekyll, so moving my content to a vanilla Jekyll site wasn't too difficult. I was happy to ditch most of the features that come with Octopress, but there were a few things I wanted to keep around. After creating a new Jekyll site and dumping all my existing posts into `_posts`, there were just a few things to set up.

## Permalinks
The most important thing to maintain during the migration was permalinks. This is just a single line in `_config.yaml`.

```yaml
permalink: /blog/:year/:month/:day/:title/
```

## Syntax Highlighting
I also wanted to keep using the same GitHub style syntax highlighting that Octopress enables by default. This is just a matter of using the `redcarpet` markdown parser, another option in `_config.yaml`.

```yaml
markdown: redcarpet
```

## Images
Images were the most annoying part. I didn't feel like adding the custom image plugin from Octopress, so I manually converted all my image tags. I also had to update `css/main.css` so images are a reasonable size.

```css
img {
  width: 100%;
}
```

## GitHub and Twitter Links
For some reason the default theme in Jekyll 2 assumes that you use the same username everywhere. This isn't the case for me, so I added the `github_user` and `twitter_user` that Octopress uses to `_config.yaml` and updated the template.

```yaml
github_user: campaul
twitter_user: cpaul37
```

## About Page and Welcome Post
Since I didn't have an about page when using Octopress, and I already had content to drop in, I just deleted `about.md` and `yyyy-mm-dd-welcome-to-jekyll.markdown`.

## Setting up GitHub Pages
This part was easy. I just added a gem containing `github-pages`, ran `bundle update`, and everything wass ready to go. No dealing with orphan branches or rake files. Now I just write, commit, and push and GitHub takes care of the rest.
