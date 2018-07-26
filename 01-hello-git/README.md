# Hello, Git!

The high level points this guide will cover are:

1. Introduction
2. Prerequisites
3. Cloning an existing Git repository
4. Committing a modified version of a file to the repository
5. Exercises

## __Introduction__

### __Origins__

Tracking changes to a document, report, or analysis helps us collaborate with
others. A simple way to track revisions of a file is to make a copy whenever
making significant changes or when sending it to a colleague for feedback.

Unfortunately, this quickly leads to situations like:

1. report.docx 
1. report new.docx
1. report new 2.docx
1. report new 3.docx
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

### __Introducing Git__

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


### __Key Concepts__

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

## __Prerequisites__

### __Tell Git who you are__

First, you need to tell Git who you are:
```
$ git config --global user.email "you@example.com"
$ git config --global user.name "Your Name"
$ git config user.email
Your Email
$ git config user.name
Your Name
```
### __Give GitHub your public keys__

1. Paste the text below, substituting in your GitHub email address. This creates a new ssh key using the provided email as a label.

```
$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```
```
Generating public/private rsa key pair.

```
2. When you're prompted to "Enter a file in which to save the key," press Enter. This accepts the default file location.

```
Enter a file in which to save the key (/c/Users/you/.ssh/id_rsa):[Press enter]

```
3. At the prompt, type a secure passphrase. Your passphrase is not visible in Git Bash window.

```
Enter passphrase (empty for no passphrase): [Type a passphrase]
Enter same passphrase again: [Type passphrase again]
```


### __Add your SSH key to the SSH-agent__

1. Ensure the SSH-agent is running:

```
$ eval $(SSH-agent -s)
Agent pid 59566
```
2. Add your SSH private key to the SSH-agent. 

```
$ ssh-add ~/.ssh/id_rsa
```

### __Add the SSH key to your GitHub account__

To configure your GitHub account to use your new SSH key, you'll also 
need to add it to your GitHub account.

1. Copy the SSH key to your clipboard. If your SSH key file has a different name than the example code, modify the filename to match your current setup. When copying your key, don't add any newlines or whitespace.

```
$ clip < ~/.ssh/id_rsa.pub
```

2. In the upper-right corner of any page, click your profile photo, then click Settings.
3. In the user settings sidebar, click SSH and GPG keys.
4. Click New SSH key or Add SSH key.
5. In the "Title" field, add a descriptive label for the new key. For example, if you're using a personal Mac, you might call this key "Personal MacBook Air".
6. Paste your key into the "Key" field.
7. Click Add SSH key.
8. If prompted, confirm your GitHub password.

Now, you are ready to create a _fork_ and clone it using git command. 

## __Clone a repository__

A _fork_ is a personal copy of a repository hosted by a provider such as
[GitHub](https://github.com). Getting a copy of a repository onto your local machine is called cloning.

```
$ git clone git@github.com:UserName/training.git
```

Now you’re in the working directory. A set of files that you currently have in front of you, are available to edit.

### __Create a new branch__

Just as you did on GitHub, once again you’re going to create a new branch, based on master for new work to go into:

```
$ git checkout -b amend-my-name
Switched to a new branch 'amend-my-name'
```

_git checkout_ is a command you’ll use a lot, to switch between branches. The _-b_ flag creates a new branch at the same time. By default, the new branch is based upon whatever branch you were on.

### __Edit a file__

1. Find a file in your working directory
1. Edit it
1. Save the edited file

### __Stage your changes__

Git has a staging area, for files that you want to commit. On GitHub when you edit a file, you commit it as soon as you save it. On your machine, you can edit a number of files and commit them altogether.

Staging a file in Git’s terminology means adding it to the staging area, in preparation for a commit.

Add your etited file to the staging area:

```
$ git add fileName
```

## __Commit your changes__

When you’re happy with your files, and have added the changes, you want to commit to the staging area:

```
$ git commit -m "added my github name"
```

The -m flag is for the message (“added my github name”) on the commit - every commit needs a commit message.

### __Push your changes to GitHub__

When you made a change on GitHub, it not only saved the change and committed the file at the same time, it also showed up right away in your GitHub repository. Here there is an extra step: we need to push the files to GitHub.

If you were pushing changes from master locally to master on GitHub, you could just issue the command git push and let Git work out what needs to go where.

It’s always better to be explicit though. What’s more, you have multiple branches here, so you need to tell git where to push (i.e. back to the remote repository you cloned from, on GitHub) and what exactly to push (your new branch).

The repository you cloned can be referred to as origin. The new branch is called amend-my-name. So:


```
$ git push origin amend-my-name
Counting objects: 34, done.
Delta compression using up to 2 threads.
Compressing objects: 100% (21/21), done.
Writing objects: 100% (28/28), 6.87 KiB, done.
Total 28 (delta 13), reused 12 (delta 7)
To git@github.com:evildmp/afraid-to-commit.git
 * [new branch]      amend-my-name -> amend-my-name
```

## __Exercises__

### 1. Creating a Fork

Create a fork and clone it.

```
$ git clone git@github.com:jawnsy/training.git
$ cd training
$ ls
```

_Tip_: We recommend using an [_SSH Key_](https://help.github.com/articles/connecting-to-github-with-ssh/)
to authenticate.

_Stuck?_ See the [GitHub documentation](https://help.github.com/articles/fork-a-repo/)
for help.

### 2. Configure Git

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

### 3. Making Changes

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

Stag the changes:

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

### 4. Sharing Changes

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
