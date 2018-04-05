## Cloning a wordpress site via valet

Prerequisites: Having a running install of [Laravel Valet](https://laravel.com/docs/5.6/valet) and the [WordPress command-line interface `wp`](http://wp-cli.org/).

1. `cd` to the directory where you have chosen to keep your valet sites.
	- You can find this directory by running `valet paths`; the appropriate directory will not be the one with `/.valet/` in its path.
	- If that command returns no appropriate directory, or no paths at all, you should create a directory on your computer to hold Valet site install directories. `mkdir ~/sites/` will create a folder named `sites` in your user's home directory. Then, run `cd ~/sites/` to go there, and `valet park` to [register this directory with Valet](https://laravel.com/docs/5.6/valet#the-park-command) so that all subdirectories will be served as `.test` domains.
2. Create the install's directory:
	- If an umbrella repo exists:
		1. `git clone git@github.com:INN/umbrella-example.git example`
		2. `git submodule update --init --recursive`
	- If you do not have a pre-existing umbrella repository, and wish to create one, follow the instructions at https://github.com/INN/umbrella-boilerplate
	- Or `mkdir example`
3. `cd example`
4. `wp core download`
5. `wp config create --dbname=example --dbuser=<user> --dbpass=<pass>`, where `<user>` and `<pass>` are the database username and password for your computer.
6. `wp db create`
	- if you're working on a multisite, you'll need to add some things to `wp-config.php`. The best way to do that is
		1. `wp core install `
		2. `wp core multisite-convert --subdomains --base=example.test --title=foo`
			- where `example.test` is the domain created by Valet for this directory
			- `--title=foo` must be passed but is unimportant and will be reset when you load the database.
7. `wp db reset`
8. download the sql file, through phpmyadmin/flywheel's interface
9. `wp db import database.sql`, replacing `database.sql` with the path to the database you downloaded
10. `wp search-replace example.org example.test --url=example.org  --all-tables-with-prefix`
	- if you're doing a multisite, make sure to rerun that command, replacing `example.org` with `subdomain.org` and `example.test` with `subdomain.example.test`, and changing the `--url=` parameter to match the valet domain that you just set everything to in the preceding search-replace:
		- `wp search-replace subdomain.org subdomain.example.org --url=example.test --all-tables-with-prefix`
		- `wp search-replace subdomain.example.org subdomain.example.org --url=example.test --all-tables-with-prefix`
		- if you're not sure what the URLs for the sites in the multisite are, check the `wp_blogs` table.
11. Optionally, run `valet secure` to serve this site locally over HTTPS using a self-signed certificate. For more about this command, see [the Laravel Valet docs](https://laravel.com/docs/5.6/valet#securing-sites).
12. Optionally, download images and uploads via SFTP. You'll probably only need the newest month's images and the images referenced in the theme settings. Feel free to upload replacement images to the new development site via the normal browser interface.
13. In the repo's child theme, if there's a `package.json`, run `npm install`
