# Github and Git version control for INN tech team and INN staff


This guide is for introducing new INN team members to Github and git version control and how we use these tools.

Start using [Github](https://github.com/) before moving on to the command line. Understand what the following terms mean:

- **repository:** n. a place where all the changes to files are stored. In github, it is a particular project within your account. In your computer, it is a particular folder where you have told git to track changes.
- **fork:**  v. copying a user's repository to your personal account; n. the copied repository; for example, if you fork *INN/docs*, the new fork will be called *your-username/docs*. Forks allow you to make changes to entire projects without affecting the original repository. To contribute to the original project, you can request the owners to integrate your work through a pull request. 
- **branch:** n.  a parallel version of a repository within the repository; unlike a fork, a branch creates an internal copy of the repository so you can make changes to the repository without affecting work in other branches. The initial and main branch is called *master*. A branch is both an internal copy of an original repository (such as *INN/docs*) as well as a branch you may create within a fork (a branch within *your-username/docs*). NOTE:  Always keep the master branch intact by creating new branches for new commits.
- **commit:** n. a changed you have authorized
- **pull request:** n. a request to merge the changes you have made in a branch within a repository or in a forked repository. A pull request may be accepted, in which case all commits are integrated, or rejected.
- **merge** v. the act of incorporating the changes from one branch (or a branch within a fork) into another. 
- **issue:** n. suggested improvements to the project. Creating an issue does not change the project; it allows you to begin a conversation about possible future changes.
- **clone:** n. a local copy of a repository in Github. v. cloning a repository in Github to your computer
- **push:** v. sending commits from a local repository to a remote repository, such as one in Github. 
- **pull:** v. fetching changes from a remote repository. If you are working with a local copy of a Github repository, you can pull the changes other users have made to that repository after you cloned it in your computer.

While you may like to fork some of the INN repositories into your own account to work on them, as a member of our team we trust you to simply create branches within INN's repositories and make commits within your branches. Once you are satisfied with the changes you have made within your branch, create a pull request so the team can merge your changes into the master branch. 

[This guide](https://github.com/INN/docs/blob/master/how-to-work-with-us/via-github.md) explains this process. Notice that Ryan forks the INN repository into his account and edits a file inside the master branch of his fork. If you are going to make many changes, it is a good idea to create a new branch within your fork (call it my-new-changes) so your master branch is clean.

**If you will not be forking an INN directory into your personal account, make sure to always create a new branch for your changes.**

![git cloning](http://inn.org/wp-content/uploads/2015/05/github-example.png)



## Git in the command line

**tl;dr:  If you are simply making changes to markdown files, such as helping with documentation, it's probably easier to stick to working in Github.com. However, if you will be working with data files and code, it's best to learn how to use git in the command line.**

If you don't have git in your computer, [follow the instructions](https://help.github.com/articles/set-up-git/) to set it up.
 
Once you understand how git works from Github.com, you can learn a bit about how to use it in the command line. Why use the command line instead of just working directly in Github.com? Well, certain changes to a directory are easier made in the command line. For example, while you can manually add new files to repositories in Github.com, you can't import files from your computer. In fact, cloning your repository to your computer and then pushing the files is the way to "import" files into Github.com. 

![git cloning](http://inn.org/wp-content/uploads/2015/05/git-clone-exampleSMALL.png)

Let's start using git commands! Pick a repository, such as INN/docs, or your fork your-user/docs, or any other repository to clone. **Please note that if you are going to clone INN/docs directly, make a new branch for any changes you make as to not directly alter the master branch.** 

1. You will start by cloning a repository into your computer. To do so, use the command line to change directories to the directory where you'd like the new repository to live. Once you are there, type
  
            git clone https://github.com/user/repository.git

   (exchange your username or the organization you are cloning from for *user* and the repository you are cloning for *repository* - you can always find this link at the bottom right of the repository.

2. You can now begin making changes to your repository. There are many git command line commands, so look over the [commands documentation](http://git-scm.com/docs) and this [simple guide](http://git-scm.com/docs) for commands.


3. If you created a fork of an INN repository, such as INN/docs that is now your-username/docs, another thing that you can't do directly in Github.com is to keep your fork in-sync with the original repository. For example, if you forked INN/docs and now have a repository called your-username/docs, after many months, your fork will be out of sync INN/docs because others will have made changes. [Here is a guide](https://help.github.com/articles/fork-a-repo/) that explains how to use the command line to sync your fork to the original repository.


Here are a few of the commands you will use the most when making changes through the command line. Please note that there are multiple commands for the same thing.

**to check the status of a repository (see if changes have been made)**

            git status
**to add all changes you have made**

            git add -A
**to commit changes you have made after adding them**

            git commit -m"type a message explaining your changes"
**to see all the commits you have made thus far**

            git log
**to see what branches exist and which branch you are using currently**

            git branch
**when a repository is cloned locally, only the master branch is tracked, so to track other branches from Github.com**

            git checkout origin/name_of_branch_to_track --track
**to change branches**

            git checkout branch-name
**to create a branch**

            git  checkout -b branch-name
**to delete a branch**

            git branch -d branch-name
**to push changes made in cloned local repository to Github.com**

            git push origin branch-name
**to pull changes made in Github.com to local repository**

            git pull origin branch-name
