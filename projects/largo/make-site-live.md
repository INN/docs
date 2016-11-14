## Taking a site from ___.wpengine.com to ___.com

1. Search and replace in the database
	- replace `___.wpengine.com` with `___.com`
	- this can be done by asking WPEngine support to do it in chat. Here are some helpful suggestions:
		- Chat subject line: "Performing search and replace in ___ install database"
		- chat general subject matter: "WordPress"
2. If there is an existing `___.com` active elsewhere in one of our installs, such as in the largoproject install:
	1. at https://my.wpengine.com/installs/largoproject/domains, where `largoproject` is the existing install, find `___.com` and delete it.
3. Add the domain to the new install.
	- https://my.wpengine.com/installs/___/domains
	- set `___.com` to be the primary
	- set `___.wpengine.com` to redirect to `___.com` by clicking "edit" next to `___.wpengine.com` and setting it to redirect to `___.com`
4. Check that you can login at the new url
5. Enable the CDN at https://my.wpengine.com/installs/___/cdn
6. If there was an existing `___.com` site in the old install:
	1. log into the old install
	2. Find the old site in http://largoproject.wpengine.com/wp-admin/network/sites.php and archive it
