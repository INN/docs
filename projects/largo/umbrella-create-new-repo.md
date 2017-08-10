This walks you through the process of creating both a new site and a new umbrella repo for that site.

## Prerequirements

- git
- access to INN's wpengine account
- permissions to create repos in INN's repos
- a working install of https://hub.github.com/
- a VVV vagrant virtualbox installed according to [INN's instructions](https://github.com/INN/docs/blob/f2d250211efc4195613e08482cdb9bc27412262f/staffing/onboarding/vvv-setup.md#L3)

## Process

1. Create site at wpengine.com. WPEngine install names cannot have dashes or periods, so drop those. Also drop the TLD. `c-hit.org` becomes `chit`. If that's not available, add back the TLD, or expand the name in other fashions. In any case, this slug will be used throughout the project and INN's internal documentation and references.
2. Read https://github.com/INN/umbrella-boilerplate/blob/master/docs/README.md
2. `vv create` and fill out the answers as apropriate, using the slug as the domain name.
3. `cd chit/htdocs`
4. `git init`
5. Create a new repository for the umbrella install, using the site name:
	1. `hub create -d "umbrella repository for c-hit.org" INN/umbrella-chit` : this should use the domain name in the description and the WPEngine slug prefixed with `INN/umbrella-`. For additional info, see `hub help create`
	2. This sets the git remote, which you can check with `git remote -v`
6. `cd ..`
7. Clone https://github.com/INN/umbrella-boilerplate someplace where you can find it
	1. follow the instructions in there: https://github.com/INN/umbrella-boilerplate/blob/master/docs/README.md
8. In my.wpengine.com, set up SFTP access:
	1. create SFTP users for the chitorg.wpengine.com install according to the instructions in INN's secrets repository
	2. add the users' details to the secrets repository
	3. update the new repo's `fabfile.py` with the appropriate secrets. There are probably instructions in that file to make your life simpler; obey them.
9. Log into the site in the umbrella and make a note of which plugins it uses.
10. Using a SFTP client, copy the used plugins in `wp-content/plugins` from the current production site to the local install.
11. Perform the first push to production
	0. Copy some files over to production manually:
		- create the 'wp-content/themes/largo' directory for the theme and upload its files
		- create the 'wp-content/plugins/client-hosting-manager' directory for the plugin and upload its files
		- upload any other plugins or submodules, be they controlled by git or not
	1. `fab production master dry_run deploy`
	2. `fab production master deploy`
	3. If those fail, you may need to create a fake .git-ftp.log:
		1. create a fake .git-ftp.log with the hash of the current commit: `git rev-parse HEAD > .git-ftp.log`
		2. upload the fake .git-ftp.log
			- cyberduck is slow and painful
			- how do we do this just with `curl`?
			- we're in cyberduck anyways, up there ^
		3. Do the same, but for the `wp-content/themes/largo/` submodule
12. Copy in the child theme(s) and any site-specific plugins that can't be installed through the Wordpress.org plugin repository
	- Make sure that the `Template:` tag in the child theme's `style.css` matches the location of Largo in `largo`
	- If a child theme or plugin is only used by the site here:
		1. git clone it, then remove the .git directory from the new thing. Make sure that the directory name matches the directory name from the installation we're copying from.
		2. add the theme's directory to the umbrella's `.gitignore` so that the theme is included and is governed by the theme's `.gitignore`, like so: https://github.com/INN/umbrella-rivard-report/blob/master/.gitignore#L81-L82
	- If a child theme or plugin is used by multiple sites (unlikely):
		1. Add it as a submodule: `git submodule add -f git://url wp-content/themes/child-theme` making sure that the pathname matches the directory name from the installation we're copying from
