## Assumptions:

This guide to updating the Largo umbrella makes the following assumptions:

- Your computer is set up [according to the onboarding documents](/staffing/onboarding/os-x-setup.md)
- Your umbrella repository is set up [according to the setup instructions](/projects/largo/umbrella-setup.md)

We'll start in the root of the largo-umbrella repository, and we're going to commit a change to the `invw` theme.

## First, check to see what's going on

    git status

You may see a message like:

    Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
      (use "git checkout -- <file>..." to discard changes in working directory)
      (commit or discard the untracked or modified content in submodules)
    
    	modified:   tools (untracked content)


This is normal! It means you have modified something in the tools/ submodule and it will be overwritten unless you save it.

    	modified:   wp-content/themes/largo-dev (new commits)
    	modified:   wp-content/themes/npq (new commits)
    	
These are themes where there are new commits locally. You should push them to their repository, but they'll stay around even if you don't.

    Untracked files:
      (use "git add <file>..." to include in what will be committed)
    
    	phpMyAdmin/
    	searchreplacedb2.php
    	wp-content/db.php

You don't need to worry about these, unless you want to `git add` them to the repository.

## Update the umbrella

    git checkout master
    git fetch
    git pull
    git submodule update --recursive
    
What you've just done is:

0. Switch to the 'master' branch of the repo
1. Copy commits from the remote repository
2. Copy the code of the current 'master' commit from the remote repo
3. Update all the submodules according to the current 'master' commit's plans.

## `git add`ing your updates

Now that the umbrella theme and all submodules are checked out and updated, you can go in and update your theme submodule's commit in the repo.

    cd wp-content/themes/invw
    git checkout master

You can substitute `master` for any other commit or branch you want to commit to the umbrella master. Just make sure that that commit or branch has been pushed to the theme's own repository on BitBucket or GitHub.

Now `cd` back to the umbrella root

    cd -
    git add wp-content/themes/invw

This will register the new submodule commit with the umbrella repo.

    git commit