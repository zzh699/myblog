---
layout: post
date: 2015-06-07 03:25   
title: Congigure a working environment on a VPS(DigitalOcean) for a django project
tags: django
---

# Congigure a working environment on a VPS(DigitalOcean) for a django project

## 1. Get a VPS host on [DigitalOcean](https://www.digitalocean.com/?utm_source=adwords&utm_medium=brand_sem&utm_campaign=Brand_Protection&utm_term=digitalocean&adgroup=&matchtype=e&network=g&device=c&position=1t1)

Need to:

1. Prepare a credit card to rent the suitalbe server. Don't worry, the cheapest monthly cost is no more than a normal lunch
2. Sign up for an account
3. follow the instructions to setup your **Droplets**. Remember to select "Django" in the "[Applications](https://cloud.digitalocean.com/droplets/new#applications)" tab under "Select Image" section.
4. Finish the rest of the instruction and login to the server no matter with the web console, ssh or putty(on Windows).

## 2. upgrade Django to the latest version

1. First, login to the server with root and run updates, as recommandded by the [official website](https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-django-with-postgres-nginx-and-gunicorn)

    $ apt-get update
    $ apt-get upgrade 

2. The default Django on the server is `1.6.1`. So we need to update it to the latest version for the [benefits](https://docs.djangoproject.com/en/1.8/howto/upgrade-version/) it provides.

    $ pip install -U Django

## 3. Configure `vim`

1. Switch to `django` account and start to configure `vim` —— the editor I love for programming

    $ su - django

2. Install [Pathogen](https://github.com/tpope/vim-pathogen) —— the vim runtimepath management tool

    $ mkdir -p ~/.vim/autoload ~/.vim/bundle && curl -LSso ~/.vim/autoload/pathogen.vim https://tpo.pe/pathogen.vim 

Add this line to you `.vimrc`

    $ echo "execute pathogen#infect()" >> ~/.vimrc

3. Install [NERDTree](https://github.com/scrooloose/nerdtree)

    $ cd ~/.vim/bundle
    $ git clone https://github.com/scrooloose/nerdtree.git

4. Finally your `.vimrc` file will look something like this:

    " common
    set nu
    set ruler
    set nocompatible
    set hlsearch

    " Pathogen related
    execute pathogen#infect()
    syntax on
    filetype plugin indent on

    " NERDTree related
    autocmd vimenter * NERDTree
    autocmd StdinReadPre * let s:std_in=1
    autocmd VimEnter * if argc() == 0 && !exists
    ("s:std_in") | NERDTree | endif
    map <C-n> :NERDTreeToggle<CR> 

## Start with your Django knowledge to rock and roll
