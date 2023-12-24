# 0x03-git

At the end of this project you should be able to reproduce and
understand the usage of these basic Git commands:
```
$ git init
$ git clone
$ git add
$ git commit
$ git status
$ git branch
$ git merge
$ git pull
$ git push
$ git checkout
$ git checkout -b
$ git log
$ git config
```
For complete list of all Git commands click [here](https://git-scm.com/docs).


## An example of how to contribute to an existing repository

A branch is like a copy of your project. It's used mainly for:
* adding a feature in development
* collaborating on the same project with other developers
* not breaking your entire repository
* not upsetting your co-workers

The purpose of a branch is to isolate your work from the main code base of your project and/or from your co-workers' work.

```
# download a repository on GitHub to our machine
# Replace `owner/repo` with the owner and name of the repository to clone
git clone https://github.com/owner/repo.git

# change into the `repo` directory
cd repo

# create a new branch to store any new changes
git branch my-branch

# switch to that branch (line of development)
git checkout my-branch

# make changes, for example, edit `file1.md` and `file2.md` using the text editor

# stage the changed files
git add file1.md file2.md

# take a snapshot of the staging area (anything that's been added)
git commit -m "my snapshot"

# push changes to github
git push --set-upstream origin my-branch
```

### An example of how to start a new repository and publish it to GitHub

First, you will need to create a new repository on GitHub. For more information, click [here](https://docs.github.com/en/get-started/quickstart/hello-world). **Do not** initialize the repository with a README, .gitignore or License file. This empty repository will await your code.

```
# create a new directory, and initialize it with git-specific functions
git init my-repo

# change into the `my-repo` directory
cd my-repo

# create the first file in the project
touch README.md

# git isn't aware of the file, stage it
git add README.md

# take a snapshot of the staging area
git commit -m "add README to initial commit"

# provide the path for the repository you created on github
git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPOSITORY-NAME.git

# push changes to github
git push --set-upstream origin main
```

### Example of how to contribute to an existing branch on GitHub

This example assumes that you already have a project called `repo` on the machine and that a new branch has been pushed to GitHub since the last time changes were made locally.

```
# change into the `repo` directory
cd repo

# update all remote tracking branches, and the currently checked out branch
git pull

# change into the existing branch called `feature-a`
git checkout feature-a

# make changes, for example, edit `file1.md` using the text editor

# stage the changed file
git add file1.md

# take a snapshot of the staging area
git commit -m "edit file1"

# push changes to github
git push
```

### Models for collaborative development
There are two primary ways people collaborate on GitHub:
1. Shared repository
2. Fork and pull

With a shared repository, individuals and teams are explicitly designated as contributors with read, write, or administrator access. This simple permission structure, combined with features like protected branches, helps teams progress quickly when they adopt GitHub.

For an open source project, or for projects to which anyone can contribute, managing individual permissions can be challenging, but a fork and pull model allows anyone who can view the project to contribute. A fork is a copy of a project under a developer's personal account. Every developer has full control of their fork and is free to implement a fix or a new feature. Work completed in forks is either kept separate, or is surfaced back to the original project via a pull request. There, maintainers can review the suggested changes before they're merged. For more information, see "[Contributing to a project](https://docs.github.com/en/get-started/exploring-projects-on-github/contributing-to-a-project)."

### How to resolve a merge conflict with a command line

You can resolve merge conflicts using the command line and a text editor.

Merge conflicts occur when competing changes are made to the same line of a file, or when one person edits a file and another person deletes the same file. For more information, see "[About merge conflicts](
https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/addressing-merge-conflicts/about-merge-conflicts)."

#### Competing line change merge conflicts
To resolve a merge conflict caused by competing line changes, you must choose which changes to incorporate from the different branches in a new commit.

For example, if you and another person both edited the file styleguide.md on the same lines in different branches of the same Git repository, you'll get a merge conflict error when you try to merge these branches. You must resolve this merge conflict with a new commit before you can merge these branches.

1. Open Terminal
2. Navigate into the local Git repository that has the merge conflict.
   > `cd REPOSITORY-NAME`
3. Generate a list of the files affected by the merge conflict. In this example, the file styleguide.md has a merge conflict.
```
$ git status
> # On branch branch-b
> # You have unmerged paths.
> #   (fix conflicts and run "git commit")
> #
> # Unmerged paths:
> #   (use "git add <file>..." to mark resolution)
> #
> # both modified:      styleguide.md
> #
> no changes added to commit (use "git add" and/or "git commit -a")
```
4. Open your favorite text editor, such as `Visual Studio Code`, and navigate to the file that has merge conflicts.
5. To see the beginning of the merge conflict in your file, search the file for the conflict marker `<<<<<<<`. When you open the file in your text editor, you'll see the changes from the HEAD or base branch after the line `<<<<<<< HEAD`. Next, you'll see `=======`, which divides your changes from the changes in the other branch, followed by `>>>>>>> BRANCH-NAME`. In this example, one person wrote "open an issue" in the base or HEAD branch and another person wrote "ask your question in IRC" in the compare branch or `branch-a.`
```
If you have questions, please
<<<<<<< HEAD
open an issue
=======
ask your question in IRC.
>>>>>>> branch-a
```

6. Decide if you want to keep only your branch's changes, keep only the other branch's changes, or make a brand new change, which may incorporate changes from both branches. Delete the conflict markers `<<<<<<<`, `=======`, `>>>>>>>` and make the changes you want in the final merge. In this example, both changes are incorporated into the final merge:
```
If you have questions, please open an issue or ask in our IRC channel if it's more urgent.
```

7. Add or stage your changes.
```git add .```

8. Commit your changes with a comment.
```git commit -m "Resolved merge conflict by incorporating both suggestions."```

You can now merge the branches on the command line or push your changes to your remote repository on GitHub and merge your changes in a pull request.

#### Removed file merge conflicts

To resolve a merge conflict caused by competing changes to a file, where a person deletes a file in one branch and another person edits the same file, you must choose whether to delete or keep the removed file in a new commit.

For example, if you edited a file, such as README.md, and another person removed the same file in another branch in the same Git repository, you'll get a merge conflict error when you try to merge these branches. You must resolve this merge conflict with a new commit before you can merge these branches.

1. Open Terminal.
2. Navigate into the local Git repository that has the merge conflict.
3. Generate a list of the files affected by the merge conflict. In this example, the file README.md has a merge conflict.
```
$ git status
> # On branch main
> # Your branch and 'origin/main' have diverged,
> # and have 1 and 2 different commits each, respectively.
> #  (use "git pull" to merge the remote branch into yours)
> # You have unmerged paths.
> #  (fix conflicts and run "git commit")
> #
> # Unmerged paths:
> #  (use "git add/rm <file>..." as appropriate to mark resolution)
> #
> #	deleted by us:   README.md
> #
> # no changes added to commit (use "git add" and/or "git commit -a")
```
4. Open your favorite text editor, such as `Visual Studio Code`, and navigate to the file that has merge conflicts.
5. Decide if you want to keep the removed file. You may want to view the latest changes made to the removed file in your text editor.

To add the removed file back to your repository:
```git add README.md```

To remove this file from your repository:
```
$ git rm README.md
> README.md: needs merge
> rm 'README.md'
```

6. Commit your changes with a comment.
```
$ git commit -m "Resolved merge conflict by keeping README.md file."
> [branch-d 6f89e49] Merge branch 'branch-c' into branch-d
```
You can now merge the branches on the command line or push your changes to your remote repository on GitHub and merge your changes in a pull request.


Learn more from GitHub docs: :point_right: [Using Git](https://docs.github.com/en/get-started/using-git).
---

**Author**: Gamachu AD
