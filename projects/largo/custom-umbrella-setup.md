# Setting up a new umbrella for a client

Clients want to develop locally and/or host outside our WPEngine account. So we can setup a new umbrella for them to make life easier.

There are two moving parts when setting up a new umbrella: the child theme repo and the new umbrella repo. 

*For the purposes of these instructions, our new child theme slug is `cornellsun` and our new umbrella repository slug is `cornell-sun`. Substitute with appropriate values.*

## 1. Create Child Theme in `largo-umbrella`

1. Login to Bitbucket 
2. Confirm you are permissioned to create new repos in projectlargo *(if you don't see an owner dropdown when you Create a repo in the web interface, ping the INN Nerds)*
3. Create a new Git repository for the child theme via web or command line. Our theme repository names are prefixed with "theme-" for clarity (ex. theme-cornellsun)
4. Submodules cannot be initialized if empty, so now is a good time to setup `style.css` in the child theme and commit up to Bitbucket.
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
#### Now it's time to initialize the repository in `largo-umbrella` in the `master` branch.
```
cd ~/largo-umbrella
git submodule add -f git@bitbucket.org:projectlargo/theme-cornellsun.git wp-content/themes/cornellsun` 
```
*Note: -f excempts the submodule from .gitignore rules. Also, don't prefix the destination directory with "theme-".*

Finally, commit these changes to `largo-umbrella`.

## 2. Create a custom umbrella for the client

1. Login to Bitbucket
2. Either fork or build a new repository based off the [custom-umbrella-boilerplate](https://bitbucket.org/projectlargo/custom-umbrella-boilerplate/src) on Bitbucket.
4. Make sure you've already [installed the proper Python tools](https://github.com/INN/docs/blob/master/projects/largo/umbrella-setup.md#3-install-python-tools), and then follow INN/deploy-tools setup instructions (including **initializing the deploy-tools submodule** in the new umbrella repo!).
5. Check WordPress prerequisites `fab wp.verify_prerequisites`
6. Install WordPress `fab wp.install:4.3.1`
7. Finally, it's time to initialize the Largo submodule and the new child theme submodule.

#### Initialize Largo
In the root directory of the new umbrella:
```
git submodule add -f git@github.com:INN/Largo.git wp-content/themes/largo
```

#### Initialize New Child Theme
In the root directory of the new umbrella:
```
git submodule add -f git@bitbucket.org:projectlargo/theme-cornellsun.git wp-content/themes/cornellsun
```

#### For good measure

After all the submodules are added, confirm they're all synced and up-to-date.
```
git submodule init && git submodule update
```

## 3. Fire up the vagrant

In the root directory of the new umbrella, run `vagrant up` to setup the vagrant machine. This will take a while.

## 4. Continue [standard umbrella setup](https://github.com/INN/docs/blob/master/projects/largo/umbrella-setup.md#8-download-production-database)

From here, you'll need to import a database, localize the URLs for use with your local development domain, and make sure your /etc/hosts file is setup for development URLs. These steps are explained [here](https://github.com/INN/docs/blob/master/projects/largo/umbrella-setup.md#8-download-production-database) the largo-umbrella setup.
