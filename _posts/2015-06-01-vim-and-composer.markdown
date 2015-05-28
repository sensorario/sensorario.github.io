---
layout: post
title:  "Vim and composer"
date:   2015-05-28
categories: vim, composer
---

<h1>Vim and composer</h1>

<p>This is my first post in this blog. I want to start here my adventure as blogger. What I want to talk about is a list of bricks I used in my first contrivute to a vim plugin. Plugin is stored here: [vim-php/vim-composer](https://github.com/vim-php/vim-composer). It aims to manage [composer](https://getcomposer.org) directly from vim. It already comes with many features, when I decided to add my personal one. Php developers, often use composer, and composer auto-generate files and know all file path. Instead of use the slowet ctag, or CtrlP, ... why dont ask to composer where files are?</p>

<h2>How to get current word in VimL</h2>
<p>I must thanks stackoverflow for this. There are several ways to take word under the cursor in Vim. <strong>expand('&lt;cword&gt;')</strong> i used in this little script.</p>

<h2>How to get the output of a bash command, from vim</h2>
<p>Oh! This is very nice. In VimL we can execute a command in bash, and get the output. When I discovered that with a grep and some awk is possible to get the position of a particular class, I've build my command to ask to composer a particular class path. That's great!</p>

<h2>How to show a meggage in vim</h2>
<p>Finally, the third think I've learned, is the way to show message in the command line. In this case, my grep/awk command can find more or less file. When grep results in more or less than one item, ... I wanted to tell users that there are not unique file in composer auto-generated file. "echo" is the command</p>

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

<h2>Pay attention to readme file</h2>
<p>Pay more and more attention to README file if you want to contribute to an open source project. User should know what you have done, reading readme file. README is automatically displayed in github project. Care about it because it must contains all information that your users should know to work with your code.</p>
<p>In some open source projet, also exists a CONTRIBUTING files. This files contains all information for developers that onw to contribute to a project. Coding standard, test informations, suggestions about [rebasing](http://git-scm.com/book/en/v2/Git-Branching-Rebasing) and [commit messages](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html).</p>
