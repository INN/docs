# Setting up a new umbrella for a client

Clients want to develop locally, but we shouldn't ask them to sync the entire largo-umbrella!

Here's how to create a client-specific umbrella to make their lives easier.

There are two moving parts when setting up a new umbrella.

## 1. Create Child Theme in `largo-umbrella`

1. Login to Bitbucket 
2. Confirm you are permissioned to create new repos in projectlargo *(if you don't see an owner dropdown when you Create a repo in the web interface, ping the INN Nerds)*
3. Create a new Git repository for the child theme via web or command line. Our theme repository names are prefixed with "theme-" for clarity (ex. theme-cornellsun)
4. Make sure the repository isn't empty (empty repos can't be initialized as submodules), so add a `style.css` file.
```
/*
Theme Name:     Cornell Daily Sun
Theme URI:      http://largoproject.org
Description:    A child theme for the The Cornell Daily Sun at Cornell University.
Author:         Institute for Nonprofit News
Author URI:     http://nerds.inn.org
Template:       largo-dev
Version:        0.1.0
*/
```

Now it's time to initialize the repository in `largo-umbrella` in the `master` branch.
```
cd ~/largo-umbrella
git submodule add -f git@bitbucket.org:projectlargo/theme-REPO-NAME.git wp-content/themes/REPO-NAME` 
```
*Note: -f excempts the submodule from .gitignore rules. Also, don't prefix the destination directory with "theme-".*

Finally, commit these changes to `largo-umbrella`.

## 2. Create a custom umbrella for the client

1. Login to Bitbucket
2. Create a new Git repository for the new umbrella via web or command line.
3. TO-DO: INSTRUCTIONS FOR FABFILE, VAGRANTFILE, ETC
4. TO-DO: Explain submodules and adding tools, largo and the child theme in `.gitmodules`
5. Run `git submodule init && git submodule update`
6.
