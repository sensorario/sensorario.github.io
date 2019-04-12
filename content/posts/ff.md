---
title: "Another tool for the git flow"
date: 2019-04-15T01:27:44+02:00
draft: true
---

## Use git faster

As developer who loves the *git flow* I created a git wrapper to be faster in version control operations. See few examples:

 - *ff feature* instead of
   - *git checkout -b feature/xxx/master*
 - *ff complete* instead of
   - *git checkout master*
   - *git merge --no-ff feature/xxx/master*
   - *git branch -D feature/xxx/master*

## Name

The name *ff* cames from the position of left-hand fingers. Those fingers should be placed over the A, S, D, and F keys.

## Nice features

 - is written with #golang
 - auto tag with *v0.0.0* if repository have no tags
 - auto increment version
   - patch in case of fixes or a refactorings
   - minor in case of new features
 - publish branch and tags
