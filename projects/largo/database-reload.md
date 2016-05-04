# Reloading Largo Umbrella Database

With some regularity it's necessary to reload the Largo Umbrella's Database.

### 1. Get a new database dump from host

```
$ fab production wp.fetch_sql_dump
```
*Pulls latest from host via SFTP -- requires INN/secrets access.*

If that fails, and if you have the secrets repo set up, you can run:

```
curl sftp://$LARGOPROJECT_PRODUCTION_SFTP_HOST:2222/wp-content/mysql.sql --user $LARGOPROJECT_PRODUCTION_SFTP_USER:$LARGOPROJECT_PRODUCTION_SFTP_PASSWORD --retry 999 --retry-max-time 0 --remote-name
```

### 2. Take vagrant snapshot

Say it with me now

```
vagrant snapshot take default the_important_safe_thing_to_do
```

To get a list of previous snapshots, use `vagrant snapshot list`. The currently-active one has a `*` next to it.

### 3. Reload SQL used in vagrant database

There are a number of relevant commands here.
* ```fab vagrant.destroy_db``` -- deletes db called largoproject
* ```fab vagrant.create_db``` -- creates MySQL db called largoproject
* ```fab vagrant.load_db:mysql.sql``` -- loads mysql.sql from largo-umbrella directory
* **fab vagrant.reload_db:mysql.sql** - Compound command that runs
    1. ```vagrant.destroy_db```
    1. ```vagrant.create_db```
    1. ```vagrant.load_db:mysql.sql```

### 4. Replace primary wp_ tables with local environment URLs

There are two ways to do this. The first uses [searchreplacedb2](https://interconnectit.com/products/search-and-replace-for-wordpress-databases/), a PHP script placed in your home directory, and the other uses [WP-CLI](http://wp-cli.org/), a command-line interface for WordPress.

#### WP-CLI

The following requires `wp-cli` version 0.23 or later. Follow [the installation instructions](http://wp-cli.org/) to make sure you've got the latest version.

```
$ vagrant up
$ vagrant ssh
vagrant@precise64:~$ cd /vagrant
vagrant@precise64:/vagrant$ wp plugin deactivate --url="largoproject.wpengine.com" redirection
vagrant@precise64:/vagrant$ wp search-replace 'largoproject.org' 'vagrant.dev' 'wp_*_options' wp_options wp_blogs wp_sitemeta
vagrant@precise64:/vagrant$ wp search-replace 'largoproject.wpengine.com' 'vagrant.dev' 'wp_*_options' wp_options wp_blogs wp_sitemeta
```

That will update all the options tables that have largoproject.wpengine.com. You will have to go back and do this later with every other site listed in [largoproject.wpengine.com/wp-admin/network/sites.php](//largoproject.wpengine.com/wp-admin/network/sites.php), because not all sites have domain names of the form `*.largoproject.wpengine.com`.

`wp plugin deactivate --url="largoproject.wpengine.com" redirection` is used to deactivate the homepage redirect that happens at `/` on the main site, which can cause problems

A breakdown of what's happening in the search-replace commands:

- `wp search-replace`: http://wp-cli.org/commands/search-replace/
- `'largoproject.org' 'vagrant.dev'`: Replace 'largoproject.org' with 'vagrant.dev' in all the tables specified
- `'largoproject.wpengine.com' 'vagrant.dev'`: Replace 'largoproject.wpengine.com' with 'vagrant.dev' in all the tables specified
- `'wp_*_options' wp_options wp_blogs wp_sitemeta`: these are the tables that the search-replace will be performed upon. `'wp_*_options'` needs version 0.23 to work properly; it failed in 0.21 because glob expansion wasn't available.

To leave the Vagrant machine, run the following:

```
vagrant@precise64:/vagrant$ exit
```

Or skip ahead to Step 5: Recreate your superadmin user

#### searchreplacedb2.php

Here we update the core WordPress tables for our multisite installation using [searchreplacedb2.php](https://interconnectit.com/products/search-and-replace-for-wordpress-databases/).

1. We need to open searchreplacedb2.php to perform kosher search and replace. If your vagrant is up, [use this link](http://vagrant.dev/searchreplacedb2.php).
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
vagrant.dev
```

### 5. Re-create your superadmin user

1. Enter the vagrant directory
```
cd ~/largo-umbrella
```
2. Remotely access your vagrant machine using ssh
```
vagrant ssh
```
3. Run the following commands
```
cd /vagrant
wp user create superadmin superadmin@vagrant.dev --role=administrator --user_pass=password
wp super-admin add superadmin
exit
```
4. Take a snapshot.

### 6. [Re-setup each member site](member-site-setup.md)
