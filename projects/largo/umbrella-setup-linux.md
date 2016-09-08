# Installing the Largo Umbrella on Linux

You should be able to follow the [OSX Setup instructions](https://github.com/INN/docs/blob/master/staffing/onboarding/os-x-setup.md) for the most part, but there are some dependencies that you *will need* to install. These instructions work if you're running Linux directly on a desktop or in a virtual machine for testing purposes.

These instructions supplement the OSX setup guide and the Largo umbrella setup guides.

These instructions assume Ubuntu 14.04, but can reasonably be adapted to any Debian-based system, and can probably be adaped to non-Debian systems if you look up the package names. Substitute your package manager of choice for `apt-get`.

## Supplements to the [INN OS X Setup Guide](https://github.com/INN/docs/blob/master/staffing/onboarding/os-x-setup.md)

In addition to the material in the OSX setup guide, you will probably find the following advice and instructions helpful.

### System updates

You're probably familiar with your package manager. Use it to fetch and apply any updates, and then reboot.

### FTP Client

Filezilla is good.

### Text editor

Sublime and gEdit are good text editors. Some of the folks at INN use vim.

```
sudo apt-get install vim
```

### Terminal emulator

The one that ships with your desktop environment is generally adequate. `xcfe4-terminal` has good unicode support; `urxvt` has better.

### Command line utilities

Assuming *Ubuntu 14.04: (You may need to modify this to suit your distro)

```
sudo apt-get install git python-pip fabric
sudo pip install virtualenv virtualenvwrapper
```

Open `~/.bashrc` and add `source /usr/local/bin/virtualenvwrapper.sh` to the very end of the file. Save and quit. Reload your `~/.bashrc` file:

```
source ~/.bashrc
```

You will need to install `curl` with support for sftp. [This is a handy script for doing just that.](https://gist.github.com/benlk/67d68631fce3d63505da)

```
wget https://gist.githubusercontent.com/benlk/67d68631fce3d63505da/raw/7cbeed142d9aff6a56b61549d42cdfcfec56481b/curl-with-sftp.sh
sudo ./curl-with-sftp.sh
cd /tmp/curl/
sudo dpkg -i curl_7*.deb libcurl3_*.deb
cd -
```

The `.deb` Debian package files output by that script are saved in your `/tmp/` directory, with *is erased upon shutdown.* You will need to reinstall those packages whenever your system updates `curl` through the package manager, so you should move them to someplace safe, like your home directory. Updates to `curl` and `libcurl` come out almost Daily on Ubuntu, so while you don't need to recompile curl every day, you should run the recompile script at least weekly.

The `wget` url in the instructions points to a known-stable version of the script, but updates may be posted to this gist: https://gist.github.com/benlk/67d68631fce3d63505da

## Supplements to the [Largo-Umbrella Local Environment](https://github.com/INN/docs/blob/99-deployment-docs/projects/largo/umbrella-setup.md) setup guide

### 3. Install Python tools.

```
sudo apt-get install pyopenssl ndg-httpsclient pyasn1 php5-cli nodejs built-essential python-dev libxml2-dev libxslt-dev zlib1g-dev lib32z1-dev libz-dev mysql-server git-ftp
```

Make sure to write down the mysql server root user's password when you set it.

```
pip install -r requirements.txt
```
