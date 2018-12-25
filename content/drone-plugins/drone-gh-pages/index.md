---
date: 2018-05-04T00:00:00+00:00
title: GitHub Pages
author: drone-plugins
tags: [ publish, github, gh-pages ]
logo: github.svg
repo: drone-plugins/drone-gh-pages
image: plugins/gh-pages
---

The GitHub Pages plugin is used to publish static websites to GitHub. The following configuration uses the gh-pages plugin to publish a website, if you are working on a private repository you don't need to provide credentials:

```yaml
kind: pipeline
name: default

steps:
- name: publish  
  image: plugins/gh-pages
  settings:
    username: octocat
    password: p455w0rd
    pages_directory: public/
```

Example configuration using credentials from named secrets:

```yaml
steps:
- name: publish  
  image: plugins/gh-pages
  settings:
    username:
      from_secret: github_username
    password:
      from_secret: github_password
    pages_directory: public/
```

Example configuration using a custom build directory:

```yaml
kind: pipeline
name: default

steps:
- name: publish  
  image: plugins/gh-pages
  settings:
    username: octocat
    password: p455w0rd
    pages_directory: public/
    temporary_base: tmp/
```

Example configuration using a custom git remote target:

```yaml
kind: pipeline
name: default

steps:
- name: publish  
  image: plugins/gh-pages
  settings:
    username: octocat
    password: p455w0rd
    pages_directory: public/
    upstream_name: upstream
```

Example configuration force pushing using a custom git remote target:

```yaml
kind: pipeline
name: default

steps:
- name: publish  
  image: plugins/gh-pages
  settings:
    username: octocat
    password: p455w0rd
    pages_directory: public/
    upstream_name: https://github.com/octocat/octocat.github.io.git
    force_push: true
```

# Parameter Reference

username
: GitHub username for pushing changes

password
: GitHub password/token for pushing changes

ssh_key
: SSH key for pushing changes

upstream_name
: GitHub upstream target, defaults to `origin`

target_branch
: GitHub target branch, defaults to `gh-pages`

force_push
: Force push to the branch, defaults to `false`

follow_tags
: Also push tags associated with commits being pushed, defaults to `false`

temporary_base
: Temporary directory to pull gh-pages branch, defaults to `.tmp`

pages_directory
: Directory of content to publish, defaults to `docs`
