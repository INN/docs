# Set up Largo-Umbrella Local Environment

NOTE: If you're setting up a new umbrella repo for a project/client, see the instructions in the largo docs: [https://largo.readthedocs.io/developers/setup.html](https://largo.readthedocs.io/developers/setup.html)

You're new to INN, or you've been here for a while and never set up the Largo Umbrella of sites before on your computer, or you've been here and have it set up but you did the setup back in the Cenozoic era and avoid doing it because you forget all the details.

Fret not! This guide will show you how to go from a Mac OS X system, with a baseline of what is described in our [setup docs](/staffing/onboarding/os-x-setup.md#terminal-emulator), and get to the point of:

* being able to browse the current version of [http://largoproject.org/](http://largoproject.org/) at the local URL [http://largo-umbrella.dev/](http://largo-umbrella.dev/)
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


## 2. Create a new WordPress install for the largoproject site  using VV

Follow the instructions in the largoproject repository: https://github.com/INN/umbrella-largoproject/blob/master/README.md

When those instructions ask you to run `fab production wp.fetch_sql_dump`, go make another cup of tea, or two. At the time of this writing, the SQL dump file was 3.1 GB. This will take at least an hour. If the download fails:

1. Run `ls *.sql` to find SQL files in your local directory
2. For the largest SQL file, run `tail largest.sql`
3. If the output of that command does not end with `-- Dump completed`, do one of the following:
	- ask someone else for their vagrant copy of the database
	- download it via a different SFTP client

When running `fab vagrant.reload_db:mysql.sql`, if you receive an error, try running the command that fab would run manually. Common causes of errors are:

- `mysql` is not installed on the host computer
- The vagrant machine needs to have its version of mysql updated: https://github.com/INN/deploy-tools/issues/51


## 3. Install Python tools.

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

## 4. Verify utility prerequisites.

There are a couple other tools that might need to be updated specifically to be able to download from and deploy to the live web sites, production and staging. Now that you have Fabric installed, you can check for those requirements and install them automatically with:

```
$ fab wp.verify_prerequisites
```
Make sure to have [git-ftp] (https://github.com/git-ftp/git-ftp/blob/develop/INSTALL.md) and the latest version of curl installed. 

## 5. Set up the secrets repository.

In order to access the live website data, you'll need to set up the INN secrets repository.

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


## 6.  Create an administrator account for yourself

1. To start, first connect to your virtual machine via ssh using

- ```vagrant ssh```

2 Navigate to your largo-umbrella install
- ```cd /srv/www/largo-umbrella/```

3 Use WP-CLI to create a new WordPress user for you
- ```wp user create superadmin superadmin@largo-umbrella.dev --role=administrator --user_pass=password```
- ```super-admin add superadmin```

That's it! Now you can logout of ssh with `exit`

## 7. Take a snapshot of the virtual machine.

Let's take a snapshot of the virtual machine as of this time when the database has just been loaded for the first time. If you make a mistake with the data and remove or modify something you didn't want to, you can revert to a snapshot much more easily than reloading the database.

Install the snapshot plugin for vagrant with:

```
$ vagrant plugin install vagrant-vbox-snapshot
```

Then take your first snapshot with:

```
$ vagrant snapshot save original_database_2015_04_09
```

You can name the snapshot anything you want, and I would recommend describing it in a short way that describes what that state would give you if you were to revert.

## 8. Get PHP tool for Database Search and Replace.

We'll be doing some work soon of searching through the database we just loaded and replacing certain values. To make this easier, download version 2.1.0 of this [database search and replace script written in PHP](https://interconnectit.com/products/search-and-replace-for-wordpress-databases/). Unzip it and move the file `searchreplacedb2.php` to your `largo-umbrella` folder.

## 9. Changing largoproject.wpengine.com to largo-umbrella.dev.

There are two ways to do this. The first uses [searchreplacedb2](https://interconnectit.com/products/search-and-replace-for-wordpress-databases/), a PHP script placed in your home directory, and the other uses [WP-CLI](http://wp-cli.org/), a command-line interface for WordPress.

#### WP-CLI

The following requires `wp-cli` version 0.23 or later. Follow [the installation instructions](http://wp-cli.org/) to make sure you've got the latest version.

```
$ vagrant up
$ vagrant ssh
vagrant@precise64:~$ cd /vagrant
vagrant@precise64:/vagrant$ wp plugin deactivate --url="largoproject.wpengine.com" redirection
vagrant@precise64:/vagrant$ wp search-replace 'largoproject.org' 'largo-umbrella.dev' 'wp_*_options' wp_options wp_blogs wp_sitemeta
vagrant@precise64:/vagrant$ wp search-replace 'largoproject.wpengine.com' 'largo-umbrella.dev' 'wp_*_options' wp_options wp_blogs wp_sitemeta
```

That will update all the options tables that have largoproject.wpengine.com. You will have to go back and do this later with every other site listed in [largoproject.wpengine.com/wp-admin/network/sites.php](//largoproject.wpengine.com/wp-admin/network/sites.php), because not all sites have domain names of the form `*.largoproject.wpengine.com`.

`wp plugin deactivate --url="largoproject.wpengine.com" redirection` is used to deactivate the homepage redirect that happens at `/` on the main site, which can cause problems

A breakdown of what's happening in the search-replace commands:

- `wp search-replace`: http://wp-cli.org/commands/search-replace/
- `'largoproject.org' 'largo-umbrella.dev'`: Replace 'largoproject.org' with 'largo-umbrella.dev' in all the tables specified
- `'largoproject.wpengine.com' 'largo-umbrella.dev'`: Replace 'largoproject.wpengine.com' with 'largo-umbrella.dev' in all the tables specified
- `'wp_*_options' wp_options wp_blogs wp_sitemeta`: these are the tables that the search-replace will be performed upon. `'wp_*_options'` needs version 0.23 to work properly; it failed in 0.21 because glob expansion wasn't available.

To leave the Vagrant machine, run the following:

```
vagrant@precise64:/vagrant$ exit
```

Or skip ahead to Step 5: Recreate your superadmin user

#### searchreplacedb2.php

Here we update the core WordPress tables for our multisite installation using [searchreplacedb2.php](https://interconnectit.com/products/search-and-replace-for-wordpress-databases/).

1. We need to open searchreplacedb2.php to perform kosher search and replace. If your vagrant is up, [use this link](http://largo-umbrella.dev/searchreplacedb2.php).
2. Leave "Pre-populate the DB values..." checked and submit.
3. Submit prefilled database information.
4. WordPress Multisite stores each member site with an ID, which can be seen prefixed in database tables. We want to select **all** the tables (probably at the bottom of the list) **without** numbered prefixes (i.e. wp_comments_meta *not* wp_55_comments_meta) and continue.
5. Find and Replace

Replace:
```
largoproject.wpengine.com
```
With:
```
largo-umbrella.dev
```

**SNAPSHOT**: Let's save our progress now. In your command line, take another snapshot with:

```
$ vagrant snapshot save after_largoproject_searchandreplace
```

#### Rock on! But wait, you're not done.

## [Complete Member Site Setup](./child-themes/new-site.md)
Each site in the Umbrella requires it's own brief setup before it can be used in a local development environment to remove production values.

## Sweet, now you're done

Now you can work with the full Largo-umbrella network of sites locally, with all of the advantages listed at the beginning of this article.

Be sure to take vagrant snapshots liberally when you make changes to the database, as they're a real timesaver in the event of making a mistake or a system crash. My system crashed with no warning while I was writing this up, and when I tried starting my virtual machine again I got an error that the virtual machine image was corrupted. I was saved a whole lot of work because I was able to just revert to the latest snapshot I had made (`vagrant snapshot restore original_database_2015_04_09`).

### You may need to [reload the database](../database-reload.md) at some point 

## Troubleshooting

If you get a redirect loop when you try to log in to [http://largo-umbrella.dev/wp-login.php](http://largo-umbrella.dev/wp-login.php) after creating the network super-admin, this may happen if the replacement of `largoproject.wpengine.com` to `largo-umbrella.dev` didn't complete. Try redoing this step.

If you don't see the "Network Admin" menu when trying to add your user to a subsite via [http://largo-umbrella.dev/wp-admin/](http://largo-umbrella.dev/wp-admin/), your network super-admin might not be so super after all. Redo the step of adding the network super-admin, only skipping the command to create the account. The command `wp super-admin add superadmin` should respond with `Success: Granted super-admin capabilities.`.

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
