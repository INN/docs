# Updating an umbrella repo from standalone Vagrant to Valet

The old standaone Vagrant installs had a Vagrantfile, which prescribed the sort of Vagrant virtual machine they were to run upon. The copy of [INN/deploy-tools](https://github.com/INN/deploy-tools/) in the umbrella you're going to upgrade has some assumptions, namely that the machine that the deploy tools use is a vagrant box at a certain IP address. When we switched to [vv and vvv](https://github.com/INN/deploy-tools/pull/48).

Here's the short list of things that need to be updated in the umbrella repo in question:

1. the copy of `INN/deploy-tools` in `tools/` needs to be updated
2. `README.md` needs new comments for either the vv/vvv setup or the Valet setup (they're funcitonally pretty similar but the details vary)
3. `.gitignore` has some new things as well

Before updating the deploy tools, we must first get the database from the existing Vagrant install. If you do not have the VM created, you may skip this section, as it's purely for maintaining the continuity of the VM on your machine.

```
$ vagrant up
$ workon largo
$ fab vagrant.dump_db
```

Now, we upgrade the repository.

```
$ cd tools/
$ pwd
/Users/benlk/inn/vms/rivard/tools
$ git status
HEAD detached at d78837a
nothing to commit, working tree clean
$ git fetch
$ git checkout master
$ git pull
Previous HEAD position was d78837a... Merge pull request #40 from INN/39-strip-surrounding-double-quotes
Switched to branch 'master'
Your branch is up-to-date with 'origin/master'.
$ cd ..
$ pwd
/Users/benlk/inn/vms/rivard
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   tools (new commits)

$ git add tools; git commit -m "Latest version of INN/deploy-tools"
```

At this point, you've updated the deploy tools to the most-recent version of the deploy tools in the repository.

To set up the new site:

1. Review the instructions at https://github.com/INN/umbrella-boilerplate/tree/master/docs/README.md We're not doing all of that.
2. From INN/umbrella-boilerplate, copy the following files into the umbrella repository:
	- .git-ftp-ignore
	- .gitignore
	- readme-template.md as README.md (or add its contents, as appropriate)
	- requirements.txt
3. If you've replaced README.md, make sure to update its contents with the appropriate names.
4. Push your changes to github.
5. Follow the setup instructions in README.md, cloning the newly-updated repository into the place where you keep your VVV or Valet installs.
6. If you're running with `yo wordpress` and Valet, run `yo wordpress` from within the post-cloning folder. Make sure that the database name you give to Yeoman matches the project name in the `fabfile.py`

### Setting up the new database

Move the dump SQL file to the root of your WordPress install.

Upload it using the appropriate method below.

Once you've uploaded it, check that the domain names in the wp_options table match the chosen local development domain.

#### VVV

Use `fab vagrant.reload_db` as described in https://github.com/INN/deploy-tools/blob/master/COMMANDS.md#database-commands

#### Valet

use `fab local.reload_db` as described in https://github.com/INN/deploy-tools/blob/master/COMMANDS.md#database-commands

If you receive an `AttributeError: local_db_user` when running that fabric command, create a file in the root of the WordPress install named `local_fabfile.py` and containing the following, with password and username adjusted as appropriate:

```
from tools.fablib import *

env.local_db_user = 'uwhatever'
env.local_db_pass = 'pwhatever'
```
