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

```
$ vagrant up
$ vagrant ssh
vagrant@precise64:~$ cd /vagrant
vagrant@precise64:/vagrant$ wp cli search-replace 'largoproject.wpengine.com' 'vagrant.dev' 'wp_*_options' wp_blogs
```

That will update all the options tables.

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
