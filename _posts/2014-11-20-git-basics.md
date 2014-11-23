---
layout 		:	post
title 		:	Git. Basics.
cover 		:   yes-github-yissssss.gif
date   		:	2014-11-24 09:15:00
align 		:
categories	:	posts
---
## Git. Basics.

As I discovered through my career, beginning developers usually not using `git` for two main reasons:

 - They think that `git` is complicated, because they never tried it.
 - They think that `git` is complicated, because they used other version control system.

This article will explain basics of git, and how you can benefit from it.

If you have not install git yet -> [http://git-scm.com/book/en/v2/Getting-Started-Installing-Git](http://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

## Preface

In this article I will use a lot of words which might be new to you.

 - *git* - is a version control system.
 - *commit* - a single record of a changes in code.
 - *repository / repo - is an object of a *git* system where code is stored, or a simply *root* folder that contains `.git` folder, or in another words your project folder.
 - *head* - is the latest commit in git tree.
 - *github* - is a website. Biggest *git* repository storage in the world. Biggest open source code storage in the world.

## Console.

Before we will start with git you will need to be introduced to the basics of `UNIX` command, that we will be used. 

 - `cd folder` is command to navigate to `folder`.
 - `touch file` is command to create `file`.
 - `mkdir folder` is command to create `folder`.
 - `rm file` is command to remove `file`
 - `rm -r folder` is command to remove `folder` (-r key stands for *recursive*).

# Git.

Lets create new folder, call it gitbeg: `mkdir gitbeg`

## Repository status aka `git status`

`git status` command return status of the repository, that include changes, branch, added/no-added files etc. Example of `git status` message:

```
 On branch master
 Changes to be committed:
 (use "git reset HEAD <file>..." to unstage)

    modified: hello.py

 Changes not staged for commit:
 (use "git add <file>..." to update what will be committed)
 (use "git checkout -- <file>..." to discard changes in working directory)

    modified: main.py

 Untracked files:
 (use "git add <file>..." to include in what will be committed)
    hello.pyc
```

You will need to remember `git status` command, as we are going to use it a lot.


## Initializing git aka `git init`

First let see what git says about **empty** folder by using `git status`.

```shell
$ git status
fatal: Not a git repository (or any parent up to mount point /home/niemand) 
```

To initialize git in the folder we need to navigate inside it

```shell
$ cd gitbeg
```

and initialize git in it.

```shell
$ git init
```

If we do now `git status`:

```
$ git status
Initialized empty Git repository in /home/niemand/gitbeg/.git/.
```

P.S. `.git` is a hidden folder used by git to repository history.

## Staging files for recording changes aka `git add`

There couple of things you need to understand about *git*. One of them is staging files. Git does not stage your files for changes, unless you add them by using `git add`. For example. Lets create new file.

```shell
$ touch example.js
```

If we do git status now:

```shell
$ git status
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)

    example.js

nothing added to commit but untracked files present (use "git add" to track)
```

Git sees that the is new file, but not recording changes. So lets add it to git:

```shell
$ git add example.js
```

and check status:

```shell
$ git status
On branch master

Initial commit

Changes to be committed:
    new file:   example.js
```

So here we go. We have added file to git.

You can add multiple files to git by:

```shell 
git add file1 file2 file3 ... filen
```

or folders of files.

```shell
git add folder1 folder2 folder3 ... foldern
```

or add it self

```shell
git add .
```

## First commit aka `git commit`.

We already have created file `example.js` lets edit it. 

Open `example.js` in your favorite editor and add there:

```javascript
console.log("Hello World!");
```

Lets check our repo:

```
$ git status
On branch master

Initial commit

Changes to be committed:
    new file:   example.js

Changes not staged for commit:
    modified:   example.js
```

Actually git lie at `Changes not staged for commit:`. The problem that file were not yet committed, but changes already done, but when we commit new file it will save changes we done to it. So lets commit the file. 

> A **commit** is a single record of a changes in code.

```
$ git commit -m "Message" file
```

```shell
$ git commit -m "My first commit! Created example.js" example.js
[master (root-commit) 0fe9521] My first commit! Created example.js.
 1 file changed, 1 insertion(+)
 create mode 100644 example.js
```

We've just made our first commit! Lets check the status:

```shell
$ git status
On branch master
nothing to commit, working directory clean
```

You thinking *"what the?"*, but the message simply says *"No changes been made, so there is nothing to commit."*. So lets go and check our history with `git log`:

```
$ git log
commit 0fe9521be422851c29f65b23db2930294b4766de
Author: Ackermann Yuriy <ackermann.yuriy@gmail.com>
Date:   Sun Nov 23 21:25:43 2014 +1300

    My first commit! Created example.js.
```

So now you can see then *key* of this commit(0fe9521be422851c29f65b23db2930294b4766de), the authors details, time stamp and message.

Lets make another commit. Open your editor and change `Hello World!` to `Hello Alice!`:

```javascript
console.log("Hello Alice!");
```

And now lets commit:

```
$ git commit -m "Changed World to Alice." example.js 
[master 323232c] Changed World to Alice.
 1 file changed, 1 insertion(+), 1 deletion(-)
```

And check history:

```
$ git log
commit 323232c96bece436201b4af82666ea0f31669187
Author: Ackermann Yuriy <ackermann.yuriy@gmail.com>
Date:   Sun Nov 23 21:35:52 2014 +1300

    Changed World to Alice.

commit 0fe9521be422851c29f65b23db2930294b4766de
Author: Ackermann Yuriy <ackermann.yuriy@gmail.com>
Date:   Sun Nov 23 21:25:43 2014 +1300

    My first commit! Created example.js.

```

Now we have two commits, and so two records in history.

### Committing multiple files

If you have situation when you changed more then one file, and you want to commit them, you have few choices.

First the `selective` method:

```
$ git commit -m "Message" file1 file2 ... filen
```

or `all` method:

```
$ git commit -am "Message"

```

The `-a` key will submit any changes in repo under one commit.

## Rolling back aka `git reset`

Imagine situation when you just submitted code with mistake, and you need to roll back to fix it. For this purposes git has `git reset` command. There two types of `reset`s:
 - Soft - uncommit but keeps the changes.
 - Hard - uncommit and not keeping the changes.

## *Soft* reset aka `git reset --soft HEAD~N`

<img src="/images/posts/git-reset-soft.png" style="float:right;padding:10px;">

Imagine we made mistake in our commit message, or forgot to add semicolon at the end of the line. But we do not want make another commit for this minor change. For that reason we have `git reset --soft`

To uncommit changes we do `git reset --soft HEAD~N` where `N` is how many head you want to be *choped off*.

So lets *soft* reset our commit:

```
$ git reset --soft HEAD~1
$ git status
Changes to be committed:

    modified:   example.js
```

So we still have changes, but if check `git log`:

```
$ git log
commit 0fe9521be422851c29f65b23db2930294b4766de
Author: Ackermann Yuriy <ackermann.yuriy@gmail.com>
Date:   Sun Nov 23 21:25:43 2014 +1300

    My first commit! Created example.js
```

There is only one commit

## *Hard* reset aka `git reset --hard HEAD~N`

<img src="/images/posts/git-reset-hard.png" style="float:right;padding:10px;">

Hard reset fully resets commits without saving any changes, *chop the heads off*. It's useful when you need to rewrite code from scratch:

```
$ git reset --hard HEAD~1
HEAD is now at 0fe9521 My first commit! Created example.js.

$ git status
On branch master
nothing to commit, working directory clean

$ git log
commit 0fe9521be422851c29f65b23db2930294b4766de
Author: Ackermann Yuriy <ackermann.yuriy@gmail.com>
Date:   Sun Nov 23 21:25:43 2014 +1300

    My first commit! Created example.js.
```

## The end.

In the next article we will talk about remote git usage.

If you want to try more visit [Try Git](https://try.github.com) course from github.