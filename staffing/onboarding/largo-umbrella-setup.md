# Set up Largo-Umbrella Local Dev Environment

You're new to INN, or you've been here for a while and never set up the Largo umbrella of sites before on your computer, or you you've been here and have it set up but you did the setup back in the Cenozoic era and avoid doing it because you forget all the details.

Fret not! This guide will show you how to go from a Mac OS X system, with a baseline of what is described in our [setup docs](/staffing/onboarding/os-x-setup.md#terminal-emulator), and get to the point of:

* being able to browse the current version of [http://largoproject.org/](http://largoproject.org/) at the local URL [http://vagrant.dev/](http://vagrant.dev/)
* being able to browse every INN member's site that uses Largo and which we host, such as [http://wisconsinwatch.org/](http://wisconsinwatch.org/) and [http://current.org/](http://current.org/), at local URLs
* having a complete local copy of the database for all aforementioned sites, which includes all site content, users, and organization.
* having a network admin account to log in to your local version of largoproject.org, which will allow you to administer your local copy of any of the INN member sites.
* having a virtual machine running on your computer that is hosting the PHP and MYSQL servers powering this local copy of WordPress, with which you can make snapshots to save states of your local sites for the ultimate Undo button.
* having a git repository set up on your computer, configured to track our private BitBucket largo-umbrella repository.
* having a copy of our deploy-tools project set up so you can, from the command line, administer the virtual machine, upgrade WordPress, download the latest copy of the production database, and deploy your changes to the staging and production sites.

Pretty cool, right?


Most of this stuff works from your command line, which you get to through the default Mac application terminal or, if you followed the setup guide, iTerm2. If you're unfamiliar with using the terminal or don't have iTerm2, be sure to go through that section in the [setup guide](/staffing/onboarding/os-x-setup.md#terminal-emulator) to get some prerequisites set up. If you have questions, be sure to ask in the INN Tech HipChat room, because the terminal can be a perplexing and idiosyncratic interface. We've all been there.

What's next?

## 1. Clone the largo-umbrella git repository hosted at BitBucket.

While we use Github for hosting our open source contributions, we use Bitbucket instead for the actual production code that powers our websites. Bitbucket allows for unlimited private repositories for Non-Profits like us, and gives us finer-grained control of permissions to individual projects.

If you haven't already, register a BitBucket account with your INN email address, and then tell Adam or Ryan that you need access to the [largo-umbrella project](https://bitbucket.org/projectlargo/largo-umbrella). If you're using the command-line interface to git, you'll need to generate an SSH key with `ssh-keygen` and save it to your Bitbucket profile settings as described [here](https://confluence.atlassian.com/display/BITBUCKET/Add+an+SSH+key+to+an+account).

When you have access to the repository, you can now clone it to your local system. The address is `git@bitbucket.org:projectlargo/largo-umbrella.git` which you can clone at the command line with:

```
$ git clone git@bitbucket.org:projectlargo/largo-umbrella.git
```

Change directory into the new `largo-umbrella` folder:

```
$ cd largo-umbrella
```

## 2. Download git submodules.

All of the member sites use Largo child themes, which are individually tracked in their own Bitbucket repositories and then linked with the largo-umbrella repository via git submodules. In addition, the INN deploy-tools, some plugins, and the Largo parent theme are included as submodules. Download them now with:

```
$ git submodule init && git submodule update
```

## 3. Install Python tools.

We use a few Python libraries for this project, including [Fabric](http://www.fabfile.org/) which powers the INN deploy-tools to elegantly run common but complex tasks. In the [OS X setup guide](/staffing/onboarding/os-x-setup.md), you should have installed Python virtualenv and virtualenvwrapper. With that as a base, create a virtual environment and install the required Python libraries:

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

## 5. Set up the secrets repository.

In order to access the live website data, and to send notifications to HipChat when you do deploy, you'll need to set up the INN secrets repository.

1. If you don't already have access to it on Github, talk to Adam or Ryan to get access. Once you get access, clone the repository to your local system:

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

## 6. Set up a virtual machine.

We use Vagrant, in conjunction with Virtual Box, to create and manage virtual machines on our development systems. If you don't have these installed yet, the [OS X setup guide](/staffing/onboarding/os-x-setup.md#virtual-machines) explains where to get them.

With Vagrant installed, start the largo-umbrella virtual machine setup process with:

```
$ vagrant up
```

Now you can go make a cup of tea and answer some emails, because this might take up to an hour. In that time, it downloads the image of a Ubuntu Linux system, installs the MySQL and PHP servers, along with all of the most recent updates, and configures it just so that all the Fabric commands work.

When it's done, edit your `/etc/hosts` file and add the following line:

```
192.168.33.10 vagrant.dev
```

This tells your system that whenever you use the address `http://vagrant.dev`, you really mean the IP address of the virtual machine.

## 7. Download WordPress.

We still need to get the WordPress core files downloaded to the right locations to tie all of this together. Based on whatever the latest version of WordPress is (4.1 at the time of writing), use Fabric to download it:

```
$ fab wp.install:4.1
```

## 8. Download production database.

Let's get the latest version of the WordPress database that powers the live, production sites. Do that with:


```
$ fab production wp.fetch_sql_dump
```

Go make another cup of tea, or two. At the time of this writing, the SQL dump file was 3.1 GB. This will take at least an hour.

## 9. Load the production database into the virtual machine.

After you've downloaded the mammoth database dump file, it's time to load it into the vagrant virtual machine. Create the database for the data to get loaded into and load the data with:

```
$ fab vagrant.create_db
$ fab vagrant.load_db:mysql.sql
```

The `vagrant.create_db` command knows what to name the database based on the `env.project_name` value set in `fabfile.py`. In this case it is `largoproject`.

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

## 12. Base configuration of WordPress.

We need to tell WordPress where to look for the database and how to access it on the virtual machine.

1. Go to [http://vagrant.dev](http://vagrant.dev), which should automatically redirect you to the config page of [http://vagrant.dev/wp-admin/setup-config.php](http://vagrant.dev/wp-admin/setup-config.php).

2. Choose your language and then go to the next screen.

3. Enter the following details for the database settings:

    * Database Name: `largoproject`
    * User Name: `root`
    * Password: `root`
    * Database Host: `localhost`
    * Table Prefix: `wp_`

4. Go to the next screen, where you have only one button to click, `Run the install`. Click that, and it will create the file `wp-config.php` in your `largo-umbrella` folder.

5. You may then see the message "Already Installed" because you already loaded the WordPress database in a previous step.

## 13. Changing largoproject.wpengine.com to vagrant.dev.

The database we downloaded from the production website has the base address, largoproject.org, hardcoded in several places. We need to update this to instead be vagrant.dev.

1. Open [http://vagrant.dev/searchreplacedb2.php](http://vagrant.dev/searchreplacedb2.php), make sure the box is checked for "Pre-populate the DB values", and click the "Submit" button.

2. The database details that filled out in the last step should appear in the form. Click the button "Submit DB details" to move on to the next step.

3. You will see a multi-select of database tables. Most will be prefixed with `wp_#_`, as opposed to `wp_`. Ctrl-click or shift-click to choose the non-number-prefixed tables. Check the box for "Leave GUID column unchanged?", and then click the "Continue" button. You may get a pop-up warning you to make sure you selected the right tables, click "OK" to continue.

4. You should now be at the screen for actually replacing the text, titled **What to replace?**. Search for `largoproject.wpengine.com` and replace with `vagrant.dev`. Click the "Submit Search string" button, and click "OK" in the pop-up to confirm that you want to do it.

**SNAPSHOT**: Let's save our progress now. In your command line, take another snapshot with:

```
$ vagrant snapshot take default after_largoproject_searchandreplace
```

## 14. Add multisite variables to WordPress config.

The file `wp-config.php` that was created by the WordPress basic configuration process is meant for a standalone site install. Largo-umbrella, on the other hand, is a special kind of WordPress site called multisite. In order for this to work for us, we need to add some variables to the file. Open `wp-config.php` in a text editor and add the following text somewhere before the last line:

```
/* Make this a multisite install. */
define('MULTISITE', true);
define('SUBDOMAIN_INSTALL', true);
define('DOMAIN_CURRENT_SITE', 'vagrant.dev');
define('PATH_CURRENT_SITE', '/');
define('SITE_ID_CURRENT_SITE', 1);
define('BLOG_ID_CURRENT_SITE', 1);
```

It's important that you add this before the last line of `require_once(ABSPATH . 'wp-settings.php');` because the variables will be ignored if you add them after.

## 15. Add a network super-admin for yourself!

When we copied down the database from the real site, we got all of the real user accounts with it. Unless you have access to the real network super-admin account on the live site, you'll need to create your own so that you can administer this local copy of the project.

At the command line, run this to access the virtual machine's command line directly:

```
$ vagrant ssh
```

Once you've connected, change directory into the `/vagrant` directory and create a new user account with the following commands:

```
$ cd /vagrant
$ wp user create superadmin superadmin@vagrant.dev --role=administrator --user_pass=password
$ wp super-admin add superadmin
$ exit
```

This will create the network super-admin with username `superadmin` and password `password`. You can use this to log in to [http://vagrant.dev/wp-login.php](http://vagrant.dev/wp-login.php).

**SNAPSHOT**: Let's save our progress now. In your command line, take another snapshot with:

```
$ vagrant snapshot take default after_adding_superadmin
```

## Almost finished...

Rock on! You now have the Largo site network set up on your computer! Continue below to get access to individual sub-sites of that network.

We'll use the shorthand `project.org` to represent a sub-site of the Largo umbrella, and you should substitute in the site you want to get access to. For example, this might instead be `investigatemidwest.org` or `iowawatch.org`.

Repeat the following sections for every sub-site that you need to access.

## 1. Add your super-admin user to `project.org`.

Even though we have a super-admin that can see all the sites, it still needs to be added manually to each site you want to administer. We'll also want to make things a little easier on ourselves when visiting the site locally, so we'll add another shortcut to our system's `/etc/hosts` file.

1. Log in to the main dashboard of your multisite via [http://vagrant.dev/wp-login.php](http://vagrant.dev/wp-login.php). In the header where it says "My Sites" open that menu and open "Network Admin" > "Sites" (or [http://vagrant.dev/wp-admin/network/sites.php](http://vagrant.dev/wp-admin/network/sites.php)).

2. Find the `project.org` site (remember to substitute in the name of the actual site you're looking for) and click on its "Edit" button.

3. Find the site's URL near the top of the page: "Edit Site: project.org" or "Edit Site: project.vagrant.dev".

4. Edit your host computer's `/etc/hosts file` by adding the line `192.168.33.10 project.vagrant.dev` to the end of the file.

5. Back in the WordPress admin, click on the "Users" tab.

6. Under "Add Existing User", enter superadmin as the username and choose the "Administrator" role.

**SNAPSHOT**: Let's save our progress now. In your command line, take another snapshot with (substitute in the name of the project):

```
$ vagrant snapshot take default after_project_adding_superadmin
```

## 2. Find the blog ID of `project.org`.

We're going to need the numeric blog ID associated with `project.org` for further steps. If you're going to be working a lot with this site, you should probably keep a cheat sheet handy.

1. Go to [http://vagrant.dev/wp-admin/network/sites.php](http://vagrant.dev/wp-admin/network/sites.php).

2. Find the `project.org` site. Click on its "Edit" button.

3. Find the site's URL near the top of the page: "Edit Site: project.org".

4. Find the ID number in the browser's current URL. For example, if the URL is `http://vagrant.dev/wp-admin/network/site-info.php?id=53` then the ID is 53. Copy this down.

## 3. Convert `project.org` to `project.vagrant.dev`.

This process is similar to what we did in replacing `largoproject.wpengine.com` with `vagrant.dev`, only we'll be selecting a different set of tables to search through based on the blog ID you now have copied down.

1. Open [http://vagrant.dev/searchreplacedb2.php](http://vagrant.dev/searchreplacedb2.php), make sure the box is checked for "Pre-populate the DB values", and click the "Submit" button.

2. You will see a multi-select of database tables. Ctrl-click or shift-click to choose the tables prefixed with `wp_#_`, where # is the blog ID you copied down. If the blog ID were 53, then you would need tables with the prefix `wp_53_`. Check the box for "Leave GUID column unchanged?", and then click the "Continue" button. You may get a pop-up warning you to make sure you selected the right tables, click "OK" to continue.

3. You should now be at the screen for actually replacing the text, titled **What to replace?**. Search for your particular `project.org` main site address and replace with `project.vagrant.dev`. For instance, if you're working with `investigatemidwest.org` then you should replace that with `investigatemidwest.vagrant.dev`. Click the "Submit Search string" button, and click "OK" in the pop-up to confirm that you want to do it.

4. If the change is successful, you should see a final summary screen with details similar to the following:

    ```
    In the process of replacing "investigatemidwest.org" with "investigatemidwest.vagrant.dev" we scanned 9 tables with a total of 18694 rows, 581 cells were changed and 579 db update performed and it all took 6.668104 seconds.
    ```

## 4. Change `project.org` to `project.vagrant.dev` in WordPress Admin.

We also need to change the settings in the Largo-umbrella network site so that `project.org` is changed to `project.vagrant.dev`. This will be the final step before we can visit `http://project.vagrant.dev` in the browser.

1. Go to [http://vagrant.dev/wp-admin/network/sites.php](http://vagrant.dev/wp-admin/network/sites.php).

2. Find the `project.org` site. Click on its "Edit" button.

3. In the **Domain** text field, change `project.org` to `project.vagrant.dev` substituting in the sub-site's actual name.

4. Click on the "Settings" tab.

5. Change the **Siteurl** text field from `http://project.org` to `http://project.vagrant.dev`.

6. Scroll all the way to the bottom and click the "Save Changes" button.

**SNAPSHOT**: Let's save our progress now. In your command line, take another snapshot with (substitute in the name of the project):

```
$ vagrant snapshot take default after_project_rename_domain
```

## Done!

Now you can work with the full Largo-umbrella network of sites locally, with all of the advantages listed at the beginning of this article.

Be sure to take vagrant snapshots liberally when you make changes to the database, as they're a real timesaver in the event of making a mistake or a system crash. My system crashed with no warning while I was writing this up, and when I tried starting my virtual machine again I got an error that the virtual machine image was corrupted. I was saved a whole lot of work because I was able to just revert to the latest snapshot I had made (`vagrant snapshot go original_database_2015_04_09`).

## Troubleshooting

If you get a redirect loop when you try to log in to [http://vagrant.dev/wp-login.php](http://vagrant.dev/wp-login.php) after creating the network super-admin, this may happen if the replacement of `largoproject.wpengine.com` to `vagrant.dev` didn't complete. Try redoing this step.

If you don't see the "Network Admin" menu when trying to add your user to a subsite via [http://vagrant.dev/wp-admin/](http://vagrant.dev/wp-admin/), your network super-admin might not be so super after all. Redo the step of adding the network super-admin, only skipping the command to create the account. The command `wp super-admin add superadmin` should respond with `Success: Granted super-admin capabilities.`.

