---
title: "git-review error: fatal: --preserve-merges was replaced by --rebase-merges"
date: 2021-11-22
---

### `git-review` error: fatal: --preserve-merges was replaced by --rebase-merges

I ran into an error with git-review that I couldn't find on the internet:

<pre class="terminal">
$ git review --version
git-review version 2.1.0
$ git --version
git version 2.34.0
$ git review
Errors running git rebase -p -i remotes/gerrit/production
fatal: --preserve-merges was replaced by --rebase-merges
It is likely that your change has a merge conflict. You may resolve it
in the working tree now as described above and then run 'git review'
again, or if you do not want to resolve it yet (note that the change
can not merge until the conflict is resolved) you may run 'git rebase
--abort' then 'git review -R' to upload the change without rebasing.
</pre>

Apparently the latest version of gerrit is incompatible with the latest version of git, due to git renaming flags.


Fortunately, the `git-review` repository has already been updated with a fix:

<pre class="terminal">
$ git clone https://opendev.org/opendev/git-review
$ cd git-review
$ git show
commit 7182166ec00ad3645821435d72c5424b4629165f
Author: Pierre Riteau <pierre@stackhpc.com>
Date:   Wed Nov 17 12:29:06 2021 +0100

    Fix use of removed --preserve-merges option

    The --preserve-merges (-p) option was replaced by --rebase-merges (-r).
    This fixes the following error when using git version 2.34.0:

        Errors running git rebase -p -i remotes/gerrit/stable/xena
        fatal: --preserve-merges was replaced by --rebase-merges
[...]
</pre>

As of November 22 2021, that commit has not yet been released to general availablity, so a source installation is currently necessary.

<pre class="terminal">
$ brew uninstall git-review
Uninstalling /usr/local/Cellar/git-review/2.1.0_1... (851 files, 11.5MB)
$ pipx install .
  installed package git-review 2.1.1.dev5, Python 3.9.8
  These apps are now globally available
    - git-review
done! ✨ 🌟 ✨
$ git-review --version
git-review version 2.1.1.dev5
</pre>

Now `git-review` works as expected.

<pre class="terminal">
$ git review
remote:
remote: Processing changes: new: 1 (\)
remote: Processing changes: new: 1 (|)
remote: Processing changes: new: 1 (/)
remote: Processing changes: new: 1 (-)
remote: Processing changes: new: 1 (\)
remote: Processing changes: refs: 1, new: 1 (\)
remote: Processing changes: refs: 1, new: 1 (\)
remote: Processing changes: refs: 1, new: 1, done
remote:
remote: SUCCESS
remote:
remote:   https://gerrit.wikimedia.org/r/c/operations/puppet/+/740712 superset: set webserver timeout to 180 seconds [NEW]
remote:
To ssh://gerrit.wikimedia.org:29418/operations/puppet.git
 * [new reference]         HEAD -> refs/for/production%topic=heads/T294771-superset-webserver-timeout
 </pre>
