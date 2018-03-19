# Prerequisites

The high level points this guide will cover are:

1. Git configuration
2. Connecting to GitHub with SSH
3. Cloning an existing Git repository
4. Committing a modified version of a file to the repository

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

### __Clone a repository__

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

### __Commit your changes__

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