---
layout: base
title:  "Settings to use git pull with rebase"
date:   2015-10-25
---

# Settings to use git pull with rebase

[This post](http://mislav.net/2013/02/merge-vs-rebase/) by [@mislav](https://github.com/mislav) does a good job of explaining benefits of rebasing when pulling, namely that `git pull --rebase` eliminates merge commits that do not communicate useful information.

There are two `git` settings that I find make this workflow smooth:

<pre>
git config --global pull.rebase true
git config --global rebase.stat true
</pre>

The first sets the default pull behavior to rebase instead of merge.

The second addresses a shortcoming of the default `rebase` behavior: unlike `merge`, `rebase` doesn't show a summary of what was pulled. Once `rebase.stat` is enabled, `git pull` shows the familiar summary diff when rebasing:

<pre class="terminal">
$ git pull
 components.js |  24 <span class="green">++++</span><span class="red">---</span>
 databases.js  |  69 <span class="green">+++++</span><span class="red">--------------</span>
 package.json  |   1 <span class="red">-</span>
 users.js      |  99 <span class="green">++++++++++++</span><span class="red">---------------</span>
 4 files changed, 86 insertions(+), 107 deletions(-)
First, rewinding head to replay your work on top of it...
Fast-forwarded unstable to 630f67cf31cab82b4cb312fb3159f5de1cbce4e7.
</pre>

See my [global gitconfig](https://github.com/razzius/personal/blob/master/.gitconfig) for other `git` settings I find useful.
