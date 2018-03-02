## Cloning a wordpress site via valet

Prerequisites: Having a running install of [Laravel Valet](https://laravel.com/docs/5.6/valet) and the [WordPress command-line interface `wp`](http://wp-cli.org/).
2. `cd` to the directory where you have chosen to keep your valet sites
4. Create the install's directory:
	- If an umbrella repo exists: `git clone git@github.com:INN/umbrella-example.git example`
	- If you do not have a pre-existing umbrella repository, and wish to create one, follow the instructions at https://github.com/INN/umbrella-boilerplate
	- Or `mkdir example`
3. `cd example`
4. `wp config create --dbname=example --dbuser=<user> --dbpass=<pass>`, where `<user>` and `<pass>` are the database username and password for your computer.
5. `wp db create`
7. `wp db reset`
5. If you have cloned an existing umbrella repository, `git submodule update --init --recursive`
6. download the sql file, through phpmyadmin/flywheel's interface
8. `wp db import database.sql`, replacing `database.sql` with the path to the database you downloaded
9. `wp search-replace example.org example.test`
10. Optionally, download images and uploads via SFTP. You'll probably only need the newest month's images and the images referenced in the theme settings. Feel free to upload replacement images to the new development site via the normal browser interface.
11. In the repo's child theme, if there's a `package.json`, run `npm install`
