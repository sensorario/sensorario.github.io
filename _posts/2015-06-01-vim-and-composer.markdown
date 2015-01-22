---
layout: post
title:  "Vim and composer"
date:   2014-08-19
categories: vim, composer
---

<h1>Vim and composer</h1>

<p>This is my first post in this blog. I want to start here my adventure as blogger. What I want to talk about is a list of bricks I used in my first contrivute to a vim plugin. Plugin is stored here: [vim-php/vim-composer](https://github.com/vim-php/vim-composer). It aims to manage [composer](https://getcomposer.org) directly from vim. It already comes with many features, when I decided to add my personal one. Php developers, often use composer, and composer auto-generate files and know all file path. Instead of use the slowet ctag, or CtrlP, ... why dont ask to composer where files are?</p>

<h2>How to get current word in VimL</h2>
<p>This is very tricky.</p>

<h2>How to get the output of a bash command, from vim</h2>

<h2>How to show a meggage in vim</h2>

<code>
function! ComposerKnowWhereCurrentFileIs()
    let l:currentWord = expand('<cword>')
    let l:command = "grep " . l:currentWord . " ./vendor/composer -R | awk '{print $6}' | awk -F\\' '{print $2}'"
    let l:commandFileFound = l:command . ' | wc -l'
    let l:numberOfResults = system(l:commandFileFound)
    if l:numberOfResults == 1
        let l:fileName = system(l:command)
        let l:openFileCommand = 'tabe .' . l:fileName
        exec l:openFileCommand
    else
        echo "No unique file found in composer's generated files"
    endif
endfunction
</code>
