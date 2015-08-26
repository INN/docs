# Git Apps for OS X

Most seasoned developers prefer using git through the Terminal for the raw power it offers.

But particularly when handling a large repository containing dozens of submodules, there are times the Terminal isn't graphic enough to illustrate intricate data about the status of a repo.

There are some great apps for graphically interacting with Bitbucket and GitHub.

Here's some good tools (as of Summer 2015).

### [GitHub Desktop](https://desktop.github.com/)

Ok this is by far the best one. Almost recommend you don't bother with the others. Paired with Terminal it's a dream.
* Clean UI for displaying repo's
* Works with GitHub out of the box and Bitbucket repos initialized via Terminal
* Undo commits easily
* Switch branches without the need to manually stash changes (switch back to `master` to check something without hassle)
* Open GitHub pull requests within the app
* Really easy "sync" button, don't worry about fetch, push, pull etc.
* Great, clean diff view
* SUPER snappy

### Adding BitBucket repos

1. First [initialize](https://confluence.atlassian.com/bitbucket/checkout-a-branch-into-a-local-repository-313466957.html) via Terminal. 
2. Install GitHub Desktop and Open.
3. Add the repo with the **+** in the upper-left corner, and choose **Add**.
4. GitHub Desktop will detect the `.git` file for the repo and load it (you'll see commits appear)
5. Note that when committing GitHub Desktop provides title and description fields -- these are combined when committing to a Bitbucket repo **just use the title**.

### [SourceTree](https://www.sourcetreeapp.com/)

Bar far the most power. It does a little too much. But provides really great in-between for Terminal-comfortable git users.

When it isn't crashing. And being a royal pain. And slow.

But powerful tools around stashing, .gitignores and other advanced functions I miss in GHD.

### [GitBox](http://www.gitboxapp.com/)

By far the least useful app, and it's paid. Sad I shelled out for it. However it does provide a very Apple Mail-esque experience for git. If you're a fan of the email flow and design pattern, this might be for you.