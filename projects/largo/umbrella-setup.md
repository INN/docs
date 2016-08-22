# Set up Largo-Umbrella Local Environment

NOTE: If you're setting up a new umbrella repo for a project/client, see the instructions in the largo docs: [https://largo.readthedocs.io/developers/setup.html](https://largo.readthedocs.io/developers/setup.html)

You're new to INN, or you've been here for a while and never set up the Largo Umbrella of sites before on your computer, or you've been here and have it set up but you did the setup back in the Cenozoic era and avoid doing it because you forget all the details.

Fret not! This guide will show you how to go from a Mac OS X system, with a baseline of what is described in our [setup docs](/staffing/onboarding/os-x-setup.md#terminal-emulator), and get to the point of:

* being able to browse the current version of [http://largoproject.org/](http://largoproject.org/) at the local URL [http://vagrant.dev/](http://vagrant.dev/)
* being able to browse every INN member's site that uses Largo and which we host, such as [http://wisconsinwatch.org/](http://wisconsinwatch.org/) and [http://current.org/](http://current.org/), at local URLs
* having a complete local copy of the database for all aforementioned sites, which includes all site content, users, and organization.
* having a network admin account to log in to your local version of largoproject.org, which will allow you to administer your local copy of any of the INN member sites.
* having a virtual machine running on your computer that is hosting the PHP and MYSQL servers powering this local copy of WordPress, with which you can make snapshots to save states of your local sites for the ultimate Undo button.
* having a git repository set up on your computer, configured to track our private BitBucket largo-umbrella repository.
* having a copy of our deploy-tools project set up so you can, from the command line, administer the virtual machine, upgrade WordPress, download the latest copy of the production database, and deploy your changes to the staging and production sites.

Pretty cool, right?

Most of this stuff works from your command line, which you get to through the default Mac application terminal or, if you followed the setup guide, iTerm2. If you're unfamiliar with using the terminal or don't have iTerm2, be sure to go through that section in the [setup guide](/staffing/onboarding/os-x-setup.md#terminal-emulator) to get some prerequisites set up. If you have questions, be sure to ask in the [INN Tech slack channel](http://slack.inn.org/), because the terminal can be a perplexing and idiosyncratic interface. We've all been there.

What's next?

## Before you get started

This guide assumes that you already have VVV setup on your machine. If you haven't setup VVV yet, follow the instructions on the [VVV Setup page](/staffing/onboarding/vvv-setup.md) before continuing.

## 1. Download production database.

Let's get the latest version of the WordPress database that powers the live, production sites.

**NOTE**: Access to the INN/secrets repo is required.

Do that with:
```
$ fab production wp.fetch_sql_dump
```

Go make another cup of tea, or two. At the time of this writing, the SQL dump file was 3.1 GB. This will take at least an hour.




## 2. Create a new site using VV

Run the following command from your vagrant root to initiate the vv site creation wizard:

```
vv create
```

Follow the prompts, entering the information below, or hitting [Enter] to skip.

Prompt | Text to enter 
------------ | -------------
Name of new site directory: | largo-umbrella 
Blueprint to use (leave blank for none or use largo): | *hit [Enter]* 
Blueprint to use (leave blank for none or use largo): | *hit [Enter]*
Domain to use (leave blank for largo-umbrella.dev): | *hit [Enter]*
WordPress version to install (leave blank for latest version or trunk for trunk/nightly version): | *hit [Enter]*
Install as multisite? (y/N): | y 
Install as subdomain or subdirectory? : | subdomain 
Git repo to clone as wp-content (leave blank to skip): | *hit [Enter]*
Local SQL file to import for database (leave blank to skip): | *This directory must be an absolute path, so the easiest thing to do is to drag your mysql file into your terminal window here and the absolute filepath with fill itself in.*
Remove default themes and plugins? (y/N): | N 
Add sample content to site (y/N): | N 
Enable WP_DEBUG and WP_DEBUG_LOG (y/N): | y
 
This will take a few minutes to build your new site and load in the database, so be patient.

## 3. Add the Largo Umbrella files to your new site

First, lets navigate to our new install using 
```
cd www/largo-umbrella/htdocs
```

Remove default wp-content folder
```
rm -rf wp-content
```

Run the following commands to initialize a new git repository and sync it with the largo-umbrella remote. This is similar to cloning a git repository, but lets us work with the files and folders we already have setup.
```
git init
git remote add origin git@bitbucket.org:projectlargo/largo-umbrella.git
git pull origin master
```

Remove the vagrant file previously used by running
```
rm Vagrantfile
```

## 4. Clone the largo-umbrella git repository hosted at BitBucket.

While we use Github for hosting our open source contributions, we use Bitbucket instead for the actual production code that powers our websites. Bitbucket allows for unlimited private repositories for Non-Profits like us, and gives us finer-grained control of permissions to individual projects.

If you haven't already, register a BitBucket account with your INN email address, and then tell Adam that you need access to the [largo-umbrella project](https://bitbucket.org/projectlargo/largo-umbrella). If you're using the command-line interface to git, you'll need to generate an SSH key with `ssh-keygen` and save it to your Bitbucket profile settings as described [here](https://confluence.atlassian.com/display/BITBUCKET/Add+an+SSH+key+to+an+account).

When you have access to the repository, you can now clone it to your local system. The address is `git@bitbucket.org:projectlargo/largo-umbrella.git` which you can clone at the command line with:

```
$ git clone git@bitbucket.org:projectlargo/largo-umbrella.git
```

Change directory into the new `largo-umbrella` folder:

```
$ cd largo-umbrella
```

## 5. Download git submodules.

All of the member sites use Largo child themes, which are individually tracked in their own Bitbucket repositories and then linked with the largo-umbrella repository via git submodules. In addition, the INN deploy-tools, some plugins, and the Largo parent theme are included as submodules. Download them now with:

```
$ git submodule init && git submodule update
```

## 6. Install Python tools.

We use a few Python libraries for this project, including [Fabric](http://www.fabfile.org/) which powers the INN deploy-tools to elegantly run common but complex tasks. In the [OS X setup guide](/staffing/onboarding/os-x-setup.md), you should have installed Python virtualenv and virtualenvwrapper.

Make sure you tell virtualenvwrapper where the umbrella is.

```
$ export WORKON_HOME=~/largo-umbrella
$ mkdir -p $WORKON_HOME
$ source /usr/local/bin/virtualenvwrapper.sh
```

Now we can create a virtual environment and install the required Python libraries:

```
$ mkvirtualenv largo-umbrella --no-site-packages
$ workon largo-umbrella
$ pip install -r requirements.txt
```

## 7. Verify utility prerequisites.

There are a couple other tools that might need to be updated specifically to be able to download from and deploy to the live web sites, production and staging. Now that you have Fabric installed, you can check for those requirements and install them automatically with:

```
$ fab wp.verify_prerequisites
```
Make sure to have [git-ftp] (https://github.com/git-ftp/git-ftp/blob/develop/INSTALL.md) and the latest version of curl installed. 

## 8. Set up the secrets repository.

In order to access the live website data, and to send notifications to HipChat when you do deploy, you'll need to set up the INN secrets repository.

1. If you don't already have access to it on Github, talk to Adam to get access. Once you get access, clone the repository to your local system:

	```
	$ git clone git@github.com:INN/secrets.git
	```

2. Add the following to the end of your shell initialization script (`~/.zshrc` if you installed Zsh, `~/.bashrc` if you kept the OS X default of bash):

	```
	source ~/src/secrets/all_secrets.sh
	```

3. Substitute in the path to where you cloned the `secrets` repository but keep `all_secrets.sh` at the end.

	Every terminal session from now on will have the secrets of the repository set as environment variables, which programs like Fabric can use so you're never prompted for a username or password.

4. To get this usable immediately, run the same command in your terminal now:

	```
	$ source ~/src/secrets/all_secrets.sh
	```


## 9.  Create an administrator account for yourself

1. To start, first connect to your virtual machine via ssh using

- ```
vagrant ssh
```

2 Navigate to your largo-umbrella install
- ```
cd /srv/www/largo-umbrella/
```

3 Use WP-CLI to create a new WordPress user for you
- ```
wp user create superadmin superadmin@vagrant.dev --role=administrator --user_pass=password
wp super-admin add superadmin
```

That's it! Now you can logout of ssh with
```
exit
```

## 10. Take a snapshot of the virtual machine.

Let's take a snapshot of the virtual machine as of this time when the database has just been loaded for the first time. If you make a mistake with the data and remove or modify something you didn't want to, you can revert to a snapshot much more easily than reloading the database.

Install the snapshot plugin for vagrant with:

```
$ vagrant plugin install vagrant-vbox-snapshot
```

Then take your first snapshot with:

```
$ vagrant snapshot take default original_database_2015_04_09
```

You can name the snapshot anything you want, and I would recommend describing it in a short way that describes what that state would give you if you were to revert.

## 11. Get PHP tool for Database Search and Replace.

We'll be doing some work soon of searching through the database we just loaded and replacing certain values. To make this easier, download version 2.1.0 of this [database search and replace script written in PHP](https://interconnectit.com/products/search-and-replace-for-wordpress-databases/). Unzip it and move the file `searchreplacedb2.php` to your `largo-umbrella` folder.

## 12. Changing largoproject.wpengine.com to vagrant.dev.

The database we downloaded from the production website has the base address, largoproject.org, hardcoded in several places. We need to update this to instead be vagrant.dev.

1. Open [http://vagrant.dev/searchreplacedb2.php](http://vagrant.dev/searchreplacedb2.php), make sure the box is checked for "Pre-populate the DB values", and click the "Submit" button.

2. The database details that filled out in the last step should appear in the form. Click the button "Submit DB details" to move on to the next step.

3. You will see a multi-select of database tables. Most will be prefixed with `wp_#_`, as opposed to `wp_`. Ctrl-click or shift-click to choose the non-number-prefixed tables. Check the box for "Leave GUID column unchanged?", and then click the "Continue" button. You may get a pop-up warning you to make sure you selected the right tables, click "OK" to continue.

4. You should now be at the screen for actually replacing the text, titled **What to replace?**. Search for `largoproject.wpengine.com` and replace with `vagrant.dev`. Click the "Submit Search string" button, and click "OK" in the pop-up to confirm that you want to do it.

**SNAPSHOT**: Let's save our progress now. In your command line, take another snapshot with:

```
$ vagrant snapshot take default after_largoproject_searchandreplace
```

#### Rock on! But wait, you're not done.

## [Complete Member Site Setup](./child-themes/new-site.md)
Each site in the Umbrella requires it's own brief setup before it can be used in a local development environment to remove production values.

## Sweet, now you're done

Now you can work with the full Largo-umbrella network of sites locally, with all of the advantages listed at the beginning of this article.

Be sure to take vagrant snapshots liberally when you make changes to the database, as they're a real timesaver in the event of making a mistake or a system crash. My system crashed with no warning while I was writing this up, and when I tried starting my virtual machine again I got an error that the virtual machine image was corrupted. I was saved a whole lot of work because I was able to just revert to the latest snapshot I had made (`vagrant snapshot go original_database_2015_04_09`).

### You may need to [reload the database](../database-reload.md) at some point 

## Troubleshooting

If you get a redirect loop when you try to log in to [http://vagrant.dev/wp-login.php](http://vagrant.dev/wp-login.php) after creating the network super-admin, this may happen if the replacement of `largoproject.wpengine.com` to `vagrant.dev` didn't complete. Try redoing this step.

If you don't see the "Network Admin" menu when trying to add your user to a subsite via [http://vagrant.dev/wp-admin/](http://vagrant.dev/wp-admin/), your network super-admin might not be so super after all. Redo the step of adding the network super-admin, only skipping the command to create the account. The command `wp super-admin add superadmin` should respond with `Success: Granted super-admin capabilities.`.

Make sure your .htaccess file contains the SubFolder configuration designed for OLD wordpress:
```
# BEGIN WordPress
RewriteEngine On
RewriteBase /
RewriteRule ^index\.php$ - [L]

# uploaded files
RewriteRule ^([_0-9a-zA-Z-]+/)?files/(.+) wp-includes/ms-files.php?file=$2 [L]

# add a trailing slash to /wp-admin
RewriteRule ^([_0-9a-zA-Z-]+/)?wp-admin$ $1wp-admin/ [R=301,L]

RewriteCond %{REQUEST_FILENAME} -f [OR]
RewriteCond %{REQUEST_FILENAME} -d
RewriteRule ^ - [L]
RewriteRule  ^[_0-9a-zA-Z-]+/(wp-(content|admin|includes).*) $1 [L]
RewriteRule  ^[_0-9a-zA-Z-]+/(.*\.php)$ $1 [L]
RewriteRule . index.php [L]
# END WordPress
```

[See the WordPress Codex](https://codex.wordpress.org/htaccess) for more.

## Local Development

Learn more about working locally in the [**INN/deploy-tools**](https://github.com/INN/deploy-tools#local-development).
