# Hello, Git!

## Origins

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


### Installing Git
Before you start using Git, you have to make it available on your computer.
click [here](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) for 
instulling on Linux, Mac and Windows.

### Tell Git who you are
First, you need to tell Git who you are:

```
$ git config --global user.email "you@example.com"
$ git config --global user.name "Your Name"
```

### Give GitHub your public keys

1- Paste the text Below, Substituting in your GitHub email address:

```
$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

This creates a new ssh key, using the provided email as a label.


```
Generating public/private rsa key pair.

```
2- When you're prompted to "Enter a file in which to save the key," press Enter. 
This accepts the default file location.


```
Enter a file in which to save the key (/c/Users/you/.ssh/id_rsa):[Press enter]

```
3- At the prompt, type a secure passphrase. Your passphrase is not visible in Git Bash window.

```
Enter passphrase (empty for no passphrase): [Type a passphrase]
Enter same passphrase again: [Type passphrase again]
```


### Adding your SSH key to the ssh-agent

1- Ensure the ssh-agent is running:


```
$ eval $(ssh-agent -s)
Agent pid 59566
```

2- Add your SSH private key to the ssh-agent. If you created your key with a different name, 
or if you are adding an existing key that has a different name, replace id_rsa in the command
 with the name of your private key file.

```
$ ssh-add ~/.ssh/id_rsa
```


###Add the SSH key to your GitHub account.
To configure your GitHub account to use your new (or existing) SSH key, you'll also 
need to add it to your GitHub account.

1- Copy the SSH key to your clipboard.
If your SSH key file has a different name than the example code, modify the filename 
to match your current setup. When copying your key, don't add any newlines or whitespace.

```
$ clip < ~/.ssh/id_rsa.pub
```

2- In the upper-right corner of any page, click your profile photo, then click Settings.
3- In the user settings sidebar, click SSH and GPG keys.
4- Click New SSH key or Add SSH key.
5- In the "Title" field, add a descriptive label for the new key. For example, if you're 
using a personal Mac, you might call this key "Personal MacBook Air".
6- Paste your key into the "Key" field.
7- Click Add SSH key.
8- If prompted, confirm your GitHub password.


Now, you are ready to create a fork and clone it using git command. Get back to Git Bash 
and type the following newlines (replace username and FolderName in the command with your
 GitHub username and your desired name, respectively).



### Clone a repository
When you made a copy of the Don’t be afraid to commit repository on GitHub, that was a fork.
A _fork_ is a personal copy of a repository hosted by a provider such as
[GitHub](https://github.com).Getting a copy of a repository onto your local machine is called 
cloning. 


```
$ git clone git@github.com:UserName/training.git
```
Now you’re in the working directory, the set of files that you currently have in front of 
you, available to edit. We want to know its status


```
$ git status
On branch master
nothing to commit (working directory clean)

```

### Create a new branch

Just as you did on GitHub, once again you’re going to create a new branch, based on master,
 for new work to go into:


```
$ git checkout -b amend-my-name
Switched to a new branch 'amend-my-name'
```

git checkout is a command you’ll use a lot, to switch between branches. The -b flag tells
 it to create a new branch at the same time. By default, the new branch is based upon whatever
 branch you were on.


### Edit a file
1- find a file in your working directory
2- Edit it
3- save the file



### Stage your changes
Git has a staging area, for files that you want to commit. On GitHub when you edit a file,
 you commit it as soon as you save it. On your machine, you can edit a number of files and 
commit them altogether.

Staging a file in Git’s terminology means adding it to the staging area, in preparation for a commit.

Add your etited file to the staging area:


```
$ git add fileName
```

### Commit your changes
When you’re happy with your files, and have added the changes you want to commit to the staging area:


```
$ git commit -m "added my github name"
```
The -m flag is for the message (“added my github name”) on the commit - every commit needs a commit message.



### Push your changes to GitHub
When you made a change on GitHub, it not only saved the change and committed the file at the same time,
 it also showed up right away in your GitHub repository. Here there is an extra step: we need to push 
the files to GitHub.

If you were pushing changes from master locally to master on GitHub, you could just issue the command
 git push and let Git work out what needs to go where.

It’s always better to be explicit though. What’s more, you have multiple branches here, so you need to
 tell git where to push (i.e. back to the remote repository you cloned from, on GitHub) and what exactly
 to push (your new branch).

The repository you cloned from - yours - can be referred to as origin. The new branch is called
 amend-my-name. So:


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

