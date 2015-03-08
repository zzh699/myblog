---
layout: post
title: Traditional Vim AutoCompletion
date: 2015-03-07 20:36
tags: vim
---

To make the most of Vim's autocomplete functionality, we need to understand two things:

- how to dial up the most relevant suggestions and
- how to choose the right word from the list.

##Meet Vim's Keyword AutoCompletion

With keyword autocompletion, Vim attempts to guess the word that we're typing, which can save us from completing it by hand

Vim's autocomplete functionality is triggered from Insert mode. When invoked, Vim builds a word list from the contents of each buffer in the current editing session and then examines the characters to the left of the cursor, looking for a partial word. If one is found, the word list is filtered to exclude anything that doesn't begin with that partial word.

###Trigger AutoCompletion.

Vim's autocompletion can be triggered form Insert mode with the <C-p> and <C-n> chords, which select the *previous* and *next* items in the word list, respectively.

There are several variant forms of autocompletion, all of which are prefixed with the <C-x> chord. You can view the complete list at `:h ins-completion`

|Command | Type of Completion|
|----------------|-----------------|
|\<C-n> | Generic keywords|
|\<C-x>\<C-n> | Current buffer keywords|
|\<C-x>\<C-i> | Included file keywords|
|\<C-x>\<C-]> | `tags` file keywords|
|\<C-x>\<C-k> | Dictionary lookup|
|\<C-x>\<C-l> | Whole line completion|
|\<C-x>\<C-f> | Filename completion|
|\<C-x>\<C-o> | Omni-completion|

`<C-x>` means hold the `Control` key and press `x`, then release both.

###The Buffer List

The simplest mechanism for population the autocomplete word list would be to use word only from the current buffer. Current file keyword completion does just that and is triggered with `<C-x><C-n>`. This can be useful when generic keyword completion generates too many suggestions and you know that the word you want is somewhere in the current buffer.

###Included Files

Most programming languages provide some way of loading code from an external file or library. in C this can be one using the `#include` directive, whereas Python uses `import` and Ruby uses `require`. If we are working on a file that includes code from another library, then it would be useful if Vim could read the contents of those referenced files when building a word list for autocompletion. And that is exactly what happens when we trigger keyword completion with the `<C-x><C-i>` command (see `:h compl=keyword`)

###Autocomplete Words from the Dictionary

*Vim's dictionary autocompletion buillds a list of suggestions from a word list. We can configure Vim so that dictionary autocompletion uses the same word list as the built-in spell checker.*

Sometimes we might want to use autocompletion on a word that isn't present in any of our open buffers, included files, or tags. In that case, we can always resort to looking up in the dictionary. This can be triggered by running the `<C-x><C-k>` command.

###Autocompletion Filenames

*When we work at the command line, we can hit the `<Tab>` key to autocomplete paths for directories and files. With filename autocompletion, we can do the same from within Vim.* Filename autocompletion is triggered by the `<C-x><C-f>` command.

Vim always maintains a reference to the *current working directory*, just like the shell. We can find out what this is at any given time by running the `:pwd` command. And we can change our working directory at any time using the `:cd {path}` command.

###Autocomplete with Context Awareness

Omni-completion is triggered with the `<C-x><C-o>` command (see:`h :compl-omni`). The functionality is implemented as a file-type plugin, so to activate it we have to source lines of configuration:

    set nocompatible
    filetype plugin on

You can fine the full list by looking up `:h compl-omni-filetypes`.

Note: for more please check the book [Practical Vim: Edit Text at the Speed of Thought](http://www.amazon.com/Practical-Vim-Thought-Pragmatic-Programmers/dp/1934356980/ref=sr_1_1?ie=UTF8&qid=1425732305&sr=8-1&keywords=vim)
