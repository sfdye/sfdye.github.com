---
title: Creating your personal static blogs in 30 minutes
date: 2017-10-09 00:00:00 +08:00
layout: single
author_profile: true
comments: true
share: true
related: true
---

By the end of this blog, you will have your own  personal blog:

- Static generated 
- Custom domain like *yourdomain.com*
- Hosted free of charge on [netlify][netlify]

## Tools used in this tutorial

- [jekyll][jekyll]
- [rbenv][rbenv] (for managing ruby environment)
- a text editor (Sublime Text  or vscode)
- (optional) a domain of your own, purchased separately from sites like GoDaddy


## Enviroment setup
Since the static site generater used here **jekyll** is written in Ruby, we will need install a Ruby development.

### System default Ruby

If you are on a Mac, ruby should be installed by the system already. You can quickly verify by:
```bash
$ which ruby
/usr/bin/ruby

$ ruby --version
ruby 2.3.3p222 (2016-11-21 revision 56859) [universal.x86_64-darwin17]
```

However, I like to install a user-maintained version of Ruby, so that I can install multiple gems without touching the system environment. **rbenv** is the tool for that, which allows you to install multiple versions of ruby and easily manage them. You can also use [rvm][rvm]. It is really a personal choice. 

### Install rbenv

If you are on a Mac, you can use brew and it can do all the magic for you.
```bash
$ brew install rbenv
```

### Install latest version of Ruby
```bash
# List all available versions to install, you will see a huge list but I will just grab 
# the latet version at the time of writing is 2.4.2
$ rbenv install --list

# Install ruby 2.4.2
$ rbenv install 2.4.2

# Run this after you install a new version of Ruby
$ rbenv rehash

# See all installed versions
$ rbenv versions
* system
2.4.2 (set by /Users/liuyang/.rbenv/version)

# Set 2.4.2 to be the default
$ rbenv global 2.4.2
system
* 2.4.2 (set by /Users/liuyang/.rbenv/version)

# Verify default is set to 2.4.2
$ which ruby
/Users/liuyang/.rbenv/shims/ruby

$ ruby --version
ruby 2.4.2p198 (2017-09-14 revision 59899) [x86_64-darwin17]
```

### Install jekyll

Now that we have ruby successully installed by rbenv, let's install the **jekyll** gem (a Ruby plugin/library).

```bash
# Install two gems jekyll and bundler
gem install jekyll bundler

# Create a new jekyll app
$ jekyll new my-blog
$ cd my-blog
$ bundle exec jekyll serve
```

Here you go, you have your first jekyll site up and running at http://localhost:4000.

Note that changes made are automatically reloaded, so you don't have to re-start the server. (not applicable to*_config.yml*)

## Install the minimal mistakes theme

The default jekyll theme [minima][mimina] is great, but I just love the [minimal mistake][mmistakes] theme designed by Michael Rose. 

It is minimalistic and fully customizable.

The [Quick Start Guide][mmistakes-guide].

Add the theme in you `Gemfile`:
```ruby
gem "minimal-mistakes-jekyll"
```

Set the theme in `_config.yml`:
```yml
theme: minimal-mistakes-jekyll
```

Run Bundler to install the theme gem and dependencies:
```bash
bundle install
```

Finally, a few clean-up:

1. Replace `<site root>/index.md` with a modified Minimal Mistakes [index.html][index.html].
2. Change layout: `post` in `_posts/0000-00-00-welcome-to-jekyll.markdown` to `layout: single`
3. Remove `about.md`

Restart jekyll server to view the changes.

## Set up Github repository

Now let's create a repostiory in your Github called `USERNAME.github.com`, like for me it's `sfdye.github.com`. If you have an existing repo, I suggest your make a backup and delete the repo to start from scratch.


Now let's commit our jekyll app to the GitHub repostory we just created.
```bash
$ git remote add origin git@github.com/USERNAME/USERNAME.github.com.git
$ git add .
$ git commit -m "First commit, Jekyll is awesome"
$ git push -u origin master

```


### Hosting your blog

There are generally three options:

1. Hosting on [GitHub Pages][ghpage]
2. Hosting on your own VPS server (AWS, heroku or Digital Ocean)
3. Use static site hosting service like [netlify][netlify] (**recommended in this tutorial**)

GitHub Pages is actually powered by jekyll behind the scene, which means you can host your jekyll app entirely on GitHub Pages for free. But this approach has some limitations. For one, it lacks the ability to use customized gem-based theme like what what are going to use in this tutorial. Hosting on your server generally means more flexibility but you have to pay for the server itself and you have to do  all the maintenance work yourself. Netlify is an awesome service for hosting personal static blog and offers features like custom domain and HTTPS, which I will cover later.


[jekyll]: https://jekyllrb.com
[netlify]: https://www.netlify.com/
[rbenv]: https://github.com/rbenv/rbenv
[rvm]: https://rvm.io/
[ghpage]: https://pages.github.com/
[mmistakes]: https://mmistakes.github.io/minimal-mistakes/
[minima]: https://github.com/jekyll/minima
[mmistakes-guide]: https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/#starting-from-jekyll-new
[index.html]: https://github.com/mmistakes/minimal-mistakes/blob/master/index.html