# Hello, Git!

## Origins

Tracking changes to a document, report, or analysis helps us collaborate with
others. A simple way to track revisions of a file is to make a copy whenever
making significant changes or when sending it to a colleague for feedback.

Unfortunately, this quickly leads to situations like:

1. report.docx
1. report new.docx
1. report new 2.docx
1. newreport.docx
1. newreport final.docx
1. newreport final final.docx

In this scheme, it can be challenging to answer simple questions like:

* Which is the latest version of the file?
* What changed between **report.docx** and **newreport.docx**?
* If we requested feedback from multiple reviewers at the same time, did we
  address everything correctly?
* If multiple collaborators modify the document concurrently, were any
  changes lost?

Many of these problems can be avoided by enforcing _mutual exclusion_ (a
scheme also called _locking_) where we ensure that only a single collaborator
can modify the document at a given time.

> _Aside_: In the early days of computing, engineers used small physical
> tokens, such as a [stuffed animal](https://en.wiktionary.org/wiki/pumpking),
> and agreed that only the person in possession of the object was allowed to
> make changes.

## Introducing Git

[Version control](https://en.wikipedia.org/wiki/Version_control) systems were
introduced to assist developers with these tasks. Early systems used a simple
[client–server](https://en.wikipedia.org/wiki/Client%E2%80%93server_model)
model, establishing a canonical, _single source of truth_ and conceptually
simplifying tracking of software revisions. These systems can feel slow when
latency is high and are unusable without network connectivity, such as on
airplanes or in rural areas.

In 2005, [Linus Torvalds](https://en.wikipedia.org/wiki/Linus_Torvalds), the
creator of the Linux kernel, released the first version of Git, which enables
developers to track changes independently on their local systems, without
relying on a centralized server. Developers can then reconcile their changes
when convenient.

## Key Concepts

Git has three _areas_:

1. The **working directory** or **workspace**: a directory containing the
   current state of a project (the latest state of the source code)
1. The **staging area**: an intermediate area where changes can be grouped,
   which can be different from the contents of the _working directory_
1. The **repository**: a hidden directory stored in the _working directory_
   (`.git`), which contains file history and other metadata about changes

In effect, `git` commands move changes between these areas. Each developer
manages their own repository, and can share changes with others by sending
or receiving changes from other repositories.

## Exercises

### Creating a Fork

A _fork_ is a personal copy of a repository hosted by a provider such as
[GitHub](https://github.com). Create a fork and clone it.

```
$ git clone git@github.com:jawnsy/training.git
$ cd training
$ ls
```

_Tip_: We recommend using an [_SSH Key_](https://help.github.com/articles/connecting-to-github-with-ssh/)
to authenticate.

_Stuck?_ See the [GitHub documentation](https://help.github.com/articles/fork-a-repo/)
for help.

### Configure Git

Configure Git with your full name and email address:

```
$ git config --global user.name "Jonathan Yu"
$ git config --global user.email "Jonathan.Yu@smartwires.com"
$ git config user.name
Jonathan Yu
$ git config user.email
Jonathan.Yu@smartwires.com
```

This configures the default name and email address to use in commit messages.
The `--global` flag causes the setting to apply to all repositories on your
system, but per-repository configuration can override these. For more detail,
see [Customizing Git](https://git-scm.com/book/tr/v2/Customizing-Git-Git-Configuration).

### Making Changes

We're collecting pictures of the cutest animals on the web. Find a picture on
a site with royalty free, public domain pictures, such as
[Pixabay](https://pixabay.com/).

Add the file to the `images/` directory and modify `Animals.md` to
display it.

Type `git status` to see what has changed:

```
$ git status
On branch master
Your branch is up to date with 'origin/master'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   Animals.md

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        images/wood-mouse-3077319_1920.jpg
```

Check changes to `Animals.md` using `git diff`:

```
$ git diff
diff --git a/01-hello-git/Animals.md b/01-hello-git/Animals.md
index 0749750..6ef3a62 100644
--- a/01-hello-git/Animals.md
+++ b/01-hello-git/Animals.md
@@ -1,3 +1,5 @@
 # Cute Animals

 ![Adorable Goats](/01-hello-git/images/goat-2216868_1920.jpg)
+
+![Adorable Mouse](/01-hello-git/images/wood-mouse-3077319_1920.jpg)
```

_Stage_ the changes:

```
$ git add Animals.md
$ git add images/wood-mouse-3077319_1920.jpg
$ git status
On branch master
Your branch is up to date with 'origin/master'.

Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   Animals.md
        new file:   images/wood-mouse-3077319_1920.jpg
```

If you run `git diff` again, there will be no output, since there are no
differences between the _working copy_ and the _staging area_:

```
$ git diff
$
```

If you want to see your changes, add `--staged`:

```
$ git diff --staged
diff --git a/01-hello-git/Animals.md b/01-hello-git/Animals.md
index 0749750..6ef3a62 100644
--- a/01-hello-git/Animals.md
+++ b/01-hello-git/Animals.md
@@ -1,3 +1,5 @@
 # Cute Animals

 ![Adorable Goats](/01-hello-git/images/goat-2216868_1920.jpg)
+
+![Adorable Mouse](/01-hello-git/images/wood-mouse-3077319_1920.jpg)
diff --git a/01-hello-git/images/wood-mouse-3077319_1920.jpg b/01-hello-git/images/wood-mouse-3077319_1920.jpg
new file mode 100644
index 0000000..84bfc98
Binary files /dev/null and b/01-hello-git/images/wood-mouse-3077319_1920.jpg differ
```

We must now _commit_ the changes to move them from the _staging area_ to our
_local repository_. Be sure to specify a descriptive message:

```
$ git commit --message="Adorable mouse"
[master e6833ec] Adorable mouse
 2 files changed, 2 insertions(+)
 create mode 100644 01-hello-git/images/wood-mouse-3077319_1920.jpg
```

_Tip_: If you omit the message, `git` will open an interactive editor.

You can view the repository's change history (the _log_), including your
change:

```
$ git log
commit e6833ec642d06b854debefdcbe1ac660ae6ab466 (HEAD -> master)
Author: Jonathan Yu <Jonathan.Yu@smartwires.com>
Date:   Fri Jan 19 15:49:27 2018 -0800

    Adorable mouse
```

### Sharing Changes

The changes have been committed to your local repository, but they not be
accessible by other team members. To make the changes visible, they need to
be _pushed_ to your _fork_:

```
$ git push
Counting objects: 12, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (11/11), done.
Writing objects: 100% (12/12), 812.48 KiB | 12.69 MiB/s, done.
Total 12 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), done.
To github.com:jawnsy/training.git
   11ba7c6..e6833ec  master -> master
```

You should now be able to browse your changes in a browser by navigating to:
https://github.com/jawnsy/training

### Creating a Pull Request

The changes have been made in your _local repository_ as well as your remote
_fork repository_ on GitHub. These changes need to be _merged_ to our shared
workspace by using a _Pull Request_. Follow GitHub's guide to
[create a pull request](https://help.github.com/articles/creating-a-pull-request/).

## See Also

* The official [Git documentation](https://git-scm.com/doc)
* [GitHub Guides](https://guides.github.com/) are all worth reading, but here
  are a few to get started:
  1. [Git Handbook](https://guides.github.com/introduction/git-handbook/)
     provides a basic introduction to Git
  1. [Hello World](https://guides.github.com/activities/hello-world/)
     explains how to get started with a GitHub account
  1. [GitHub Flow](https://guides.github.com/introduction/flow/) explains the
     ‘GitHub recommended’ workflow — Smart Wires Analytics has modeled our
     workflow on the GitHub Flow
* [Bitbucket Guides](https://www.atlassian.com/git/tutorials/what-is-version-control)
* [Git From the Bits Up](https://youtu.be/MYP56QJpDr4): a fun talk about how
  Git works internally. The presenter manually creates a working Git
  repository from scratch by creating all of the files under `.git`
