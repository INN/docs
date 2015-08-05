# Reloading Largo Umbrella Database

With some regularity it's necessary to reload the Largo Umbrella's Database.

### 1. Get a new database dump from host

```
$ fab production wp.fetch_sql_dump
```
*Pulls latest from host via SFTP -- requires INN/secrets access.*

### 2. Take vagrant snapshot

Say it with me now

```
vagrant snapshot take default the_important_safe_thing_to_do
```

### 3. Reload SQL used in vagrant database

There are a number of relevant commands here.

* ```fab vagrant.create_db``` -- creates MySQL db called largoproject
* ```fab vagrant.destroy_db``` -- deletes db called largoproject
* ```fab vagrant.load_db:mysql.sql``` -- loads mysql.sql from largo-umbrella directory
* **fab vagrant.reload_db:mysql.sql** - Compound operation that runs
    1. ```vagrant.destroy_db```
    1. ```vagrant.create_db```
    1. ```vagrant.load_db:mysql.sql```

### 4. Replace primary wp_ tables with local environment URLs

Here we update the core WordPress tables for our multisite installation using searchreplacedb2.php.

1. We need to open searchreplacedb2.php to perform kosher search and replace. If you're vagrant is up, [use this link](http://vagrant.dev/searchreplacedb2.php).
2. Leave "Pre-populate the DB values..." checked and submit.
3. Submit prefilled database information.
4. WordPress Multisite stores each member site with an ID, which can be seen prefixed in database tables. We want to select **all** the tables (probably at the bottom of the list) **without** numbered prefixes (i.e. wp_comments_meta *not* wp_55_comments_meta) and continue.
5. Find and Replance

Replace:
```
largoproject.wpengine.com
```
With:
```
vagrant.dev
```

### 5. Recreate your superadmin user

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

### 6. Resetup each member site

Link pending...
