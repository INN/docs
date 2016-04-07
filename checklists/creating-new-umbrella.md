## Creating a new umbrella repository

Most of the steps can be found in the Largo docs, under [Setting up a complete Largo dev environment](https://largo.readthedocs.org/developers/setup.html).

Some notes:

- On step 2, when creating a new umbrella, it may be easier to put Largo in `largo-dev`.
- On step 4, rename the following files:
	- `git-ftp-ignore` -> `.git-ftp-ignore`
	- `gitignore` -> `.gitignore`
- After step 4:
	1. Add this site's SFTP username, password, and host to the secrets repository, following the style of those files to add those values as environment variables. If you are uncertain about the host, check the site's dashboard on my.wpengine.com.
	2. Edit the new umbrella's `fabfile.py` to match [the `largo-umbrella` one](https://bitbucket.org/projectlargo/largo-umbrella/src/master/fabfile.py). Of note:
		- [ ] `import os`
		- [ ] `env.sftp_deploy = True`
		- [ ] production host, user, password, domain and port added
		- [ ] staging host, user, password, domain and port added
		- the port is 2222 for WP Engine
		- the domain is the URL
		- [ ] `env.project_name` needs a name
		- [ ] the `env.domain` blockthe project name

## Deploying the new umbrella for the first time

If you receive an error such as the following:

```
$ fab master production dry_run deploy
[localhost] Executing task 'master'
On master
[localhost] Executing task 'production'
[45.79.65.60] Executing task 'dry_run'
[45.79.65.60] Executing task 'deploy'
Currently-deployed commit: dd6027bc3c7ae11b516d022dccedb38ef4609548
Setting rollback point...
Deploying...

Warning: local() encountered an error (return code 1) while executing 'git remote -v | grep -E "production.*production/kinseycon.*$"'

Adding remote for "production"
FATAL: W any production/kinseycon largoproject-bkeith DENIED by fallthru
(or you mis-spelled the reponame)
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.

Done.
```

You have not set `env.sftp_deploy = true` in your umbrella's `fabfile.py`

If you receive this error:

```
$ fab master production dry_run deploy
[localhost] Executing task 'master'
On master
[localhost] Executing task 'production'
[45.79.65.60] Executing task 'dry_run'
[45.79.65.60] Executing task 'deploy'
[45.79.65.60] download: <file obj> <- /.git-ftp.log

Warning: get() encountered an exception while downloading '/.git-ftp.log'

Underlying exception:
    No such file

Currently-deployed commit: None
No rollback commit found. Unable to set rollback point.
Checking out branch: master
Deploying...
fatal: Dirty repository: Having uncommitted changes. Exiting...
Found no existing git repo on ftp host, initializing...
fatal: Dirty repository: Having uncommitted changes. Exiting...
An error occurred...
Try deploying with `verbose` for more information...

Done.
Disconnecting from 45.79.65.60:2222... done.
```

Your submodules are dirty. Dirty means [that there are uncomitted changes or untracked files in the submodule](http://longair.net/blog/2010/06/02/git-submodules-explained/#changes-in-1.7.0).

You must perform the following steps:

1. Using an FTP client, compare the submodules in your local umbrella repo to the production site:
	- if the submodule's folder does not exist, create it, and perform the next step:
	- if the submodule's folder exists on the remote server, use the FTP client to copy the entire contents of the submodule to the production site. Save time by **not** copying `.git` or `node_modules` over.
2. re-run `fab production master dry_run deploy` to ensure that the remote repository is not dirty.
	- If it is still dirty, continue copying files manually from the local umbrella to the remote server until it is no longer dirty.
3. Once the remote repo is no longer dirty, remove the `dry_run` and run `fab production master deploy` to actually deploy
4. Commit a change to the umbrella and re-deploy, to make sure that the deploy actually works.
5. Do not forget to push your changes to the appropriate remote version control server.
