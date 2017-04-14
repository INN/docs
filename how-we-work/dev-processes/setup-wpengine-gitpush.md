# How to Setup Git-Push on WP Engine

* This guide assumes you are setting up a new site on your local environment, and uses Valet by default (but can be adapted for any local development setup).

## Setting up Git-Push Access with WP Engine
1. Open up your terminal.
2. Run `cat ~/.ssh/id_rsa.pub | pbcopy` in your terminal. This will copy your ssh key to your clipboard.
3. Visit http://my.wpengine.com, select the install you're working on, then select "Git push" from the left-hand menu.
4. Paste your ssh key into the textfield and enter your name. (Once you enter your SSH key and set your name, that name will be the same for every install).

## Setting up your local environment
1. In terminal, navigate to where you'd like to host your site on your computer
2. Clone the umbrella repo using the `--recursive` flag, like so: ` git clone --recursive https://github.com/INN/umbrella-innlabs`
  - This will clone your site and setup Staging as the default push location (for safety).
  - The `--recursive` flag will also download any submodules present in the repo.
3. Run `git remote add staging git@git.wpengine.com:staging/install.git`, where `install` is the name of your WP Engine site.
  - This will allow you to push changes to the staging site.
4. Run `git remote add production git@git.wpengine.com:production/install.git`, where `install` is the name of your WP Engine site.
  - This will allow you to push changes to the production site.
6. Run `yo wordpress` to build a copy of WordPress around this, filling in the details as you normally would.

## Using Git-Push
When you've made changes you want to push to staging or production, simply commit them and push them (as you would normally).
- To push the contents of the master branch to staging, use `git push staging master`.
- To push the contenst of the master branch to production, use `git push production master`.
