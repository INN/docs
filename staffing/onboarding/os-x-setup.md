# OS X Setup for News Apps Development

On a new OS X workstation, it's helpful to get a baseline level of software installed before jumping into the deep end of News Apps Development at INN.

## Security

It's a really good idea to encrypt the hard drive using the [FileVault feature](https://support.apple.com/en-us/HT4790), and it's offered by default on a new OS X setup. By default, this uses your iCloud password for encryption. Set your password to something challenging, which you should be doing anyway.

## Backup

After you encrypt your drive, it's imperative that you have a regular backup strategy. I worked for 11 years in tech support, helping people recover data from their crashed laptop hard drives after accidentally running over their laptops in the car, and it was only possible if the drive wasn't encrypted. The odds of data recovery were still pretty bad, but the people who were already backing up didn't skip a beat in getting back to work. Your laptop is not your work, it's just a handy set of tools.

If nothing else, get an external hard drive that you leave at home and set up [Time Machine](https://support.apple.com/en-us/HT201250) to back up to it. Set a calendar reminder to do this regularly (aim for doing this daily). You could also back up to a Network Attached Storage on your home network, which would work over the wireless connection. Apple sells one called an [AirPort Time Capsule](http://store.apple.com/us/product/ME177LL/A/airport-time-capsule-2tb").

Any files you're using that are shared interest to the company, work on them in Dropbox. For your coding projects, be sure to be regularly pushing your commits or branches to Github/Bitbucket.

## System Updates

Install all OS X system software updates, all of them until you go blue in the face. At no time other than right now, with a computer that has nothing interesting or fun running on it yet, is it going to be less annoying to do a series of reboots. Just get it over with; install other software while this is going on, but reboot as often as you need in order to get up to date. Putting this off just leads to pain later.

## System Preferences

Look through the OS X System Preferences and make a few choices. Perhaps you have personal preferences about how notifications do/don't appear, what the screensaver looks like, what hot corners do (what happens when you put your mouse cursor in the corner of a screen), or that the "Quack" sound should be used for all alerts. You can always make adjustments later, but you might as well explore what the computer can do. You chose to make news apps because you are curious and want to change things, remember?

## Web Browsers

Install additional web browsers. Safari is a fine browser, but when writing and testing web applications, it makes no sense to have only one browser installed. I install [Google Chrome](https://www.google.com/chrome/) and [Mozilla Firefox](https://www.getfirefox.com/). Choose your preferred default browser and make sure you never get nagged again by the others.

## FTP Client

You may not need the FTP client immediately, but when you do need to access an FTP server you'll be glad you already have a client. You can use FTP from the command line, but I find that experience to be akin to doing a road trip in a horse and buggy cart. Do yourself a favor, install [Cyberduck](https://cyberduck.io), and ride in style with air conditioning and power steering.

If you are using git-ftp and are experiencing problems deploying with the deploy-tools scripts, try using git-ftp version 0.9.0. ``git-ftp --version`` will tell you what version you are on.

## Text Editor

If you already have a favorite text editor, feel free to skip this section. If you are open to trying new things, or are looking for a recommendation, then I highly recommend you install [Sublime Text](http://www.sublimetext.com/). It's free, is beginner-friendly, and using it makes me feel like I'm driving a space ship. I originally installed it for the [color](https://packagecontrol.io/browse/labels/color%20scheme) [schemes](https://github.com/daylerees/colour-schemes) [which](http://tmtheme-editor.herokuapp.com/#/theme/Monokai) [abound](http://colorsublime.com/).

I also recommend installing the [Package Control](https://packagecontrol.io/installation#st2) for Sublime Text, which then gives you access to [a bunch of nifty tools](https://packagecontrol.io/) that plug into the editor.

## Terminal Emulator

The default terminal emulator that comes with OS X is okay, but I like pretty color schemes and it seems easier to do this in [iTerm2](http://iterm2.com/). Anyway, there are more options and it's pretty popular, and it's free.

With either the default terminal emulator or iTerm2, create a new terminal and install some things you'll use there.

## Command Line Utilities

Start with the command-line tools you'll need to use for further terminal goodness. You can install that by running `xcode-select --install` and following the instructions that appear to install the offered command-line tools.

[Homebrew](http://brew.sh/) is so useful, I wouldn't be surprised if it was included in OS X in the future. It's a command-line package manager with a simple interface that lazy people like me can use. When I want to install a new CLI tool, and I don't want to deal with the tomfoolery of finding all the dependencies and the latest download link, I can usually do it with Homebrew. Get Homebrew with `ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`.

Let's install MySQL, to be able to work with MySQL databases in the future. `brew install mysql`. Yup, that's it. There are some instructions it supplies you after completing the install about getting the MySQL server to start automatically or manually.

[Wget](http://www.gnu.org/software/wget/) is a command-line tool for retrieving files using HTTP(S) and FTP. It's as simple as `brew install wget`. It's useful for the basics or [creating a flat mirror](http://fosswire.com/post/2008/04/create-a-mirror-of-a-website-with-wget/) of a dynamic site.

[phpunit](https://phpunit.de/) is a unit testing tool for PHP that INN uses for unit testing in WordPress.

    wget https://phar.phpunit.de/phpunit.phar
    chmod +x phpunit.phar
    mv phpunit.phar /usr/local/bin/phpunit

Will Haynes' post [Unit Testing Themes and Plugins in WordPress](http://nerds.inn.org/2014/10/22/unit-testing-themes-and-plugins-in-wordpress/) on INN Nerds outlines additional dependencies (see Step Two) and WordPress-specific elements.

Later, we'll be using Python for a few projects, and the way to keep Python library versions and environments organized with different projects is to use[virtualenv](https://virtualenv.pypa.io/en/latest/) and [virtualenvwrapper](https://virtualenvwrapper.readthedocs.org/en/latest/). To install those, we need to first install the [pip](https://pip.pypa.io/en/latest/) Python package manager, and then we'll install the virtualenv packages with pip. Run `sudo easy_install pip && sudo pip install virtualenv virtualenvwrapper` in your terminal.

You're also going to want to install [node](https://nodejs.org/) (`brew install node`) which will get you the [node package manager](https://www.npmjs.com/) and [grunt](http://gruntjs.com/) (`npm install -g grunt-cli`) which we'll use a bit later for [asset minification](http://whatis.techtarget.com/definition/code-minification-minify) and other tasks in working on our projects.

If you installed Sublime Text, it's nice to be able to invoke it from the command line, like `subl README.md`. We can create a `subl` alias by using [these instructions](https://www.sublimetext.com/docs/2/osx_command_line.html).

We might as well generate an SSH key now, which we'll eventually use with Bitbucket and Github so we don't have to log in from the command line when pushing to those repositories. Generate an SSH key using the command `ssh-keygen`. The contents of `~/.ssh/id_rsa.pub` is what you can use for your [Github](https://help.github.com/articles/generating-ssh-keys/) and [Bitbucket](https://confluence.atlassian.com/display/BITBUCKET/Add+an+SSH+key+to+an+account) account settings. (If you've already generated an ssh key on another computer and added it to Github and Bitbucket, copy your `~/.ssh` folder to the machine you're using for development.)

Since we're on the topic of git, you should configure your name and email globally that you'll be using with Github/Bitbucket. Following [these instructions](http://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup#Your-Identity) from the official Git documentation book, you can do it like this:

    git config --global user.name "Nick Bennett"
    git config --global user.email nick@inn.org


## Local Server Environment

There are two basic ways of setting up a local server environment for development and testing.

If you're not a developer, the easiest method is to work on our projects is to use [MAMP](https://www.mamp.info). MAMP is an application that uses your existing operating system to build a server environment on your computer.

- [MAMP Setup Instructions](/staffing/onboarding/mamp-setup.md)

For developers, Vagrant is a more advanced configuration that allows us to mirror our production environment locally and test our code more comprehensively. We use [VirtualBox](https://www.virtualbox.org/wiki/Downloads) and [Vagrant](https://www.vagrantup.com/downloads.html) to build virtual machines that simulate the server environments where our work will be publicly hosted. To help us setup Vagrant for WordPress development, we use [VVV](https://github.com/varying-vagrant-vagrants/vvv/), which simplifies the setup of our Vagrant box and gives us a quick-start with a slew of features for WordPress development.

- [Vagrant Setup Instructions](/staffing/onboarding/vvv-setup.md)

For a real-world example of using VirtualBox, Vagrant, and VVV, check out our documentation on [Setting up a complete Largo dev environment](http://largo.readthedocs.io/developers/setup.html).

## Deploy Tools

We use a [Fabric](http://www.fabfile.org) for deployment and to automate common tasks in our development workflow. Visit our [deploy-tools project on Github](https://github.com/INN/deploy-tools#the-basics) to learn more about this setup. we use this for every one of our WordPress site projects. If you are developing a WordPress site, we highly recommend checking this out to streamline your development and deployment process.

## Communications

Working remotely full-time only works if we're all in constant communication. [We use a host of tools](/how-we-work/tools.md) for this, most of them are browser-based. You can use [Slack](//www.slack.com) in the browser, you can also download the mobile app. 

Dropbox is another tool we use that really begs for a native client to be installed. Dropbox is like the shared network drive so common to Windows-based networks, only the files actually go on your computer instead of accessing them through some tenuous ethereal connection. This is why [FileVault](https://support.apple.com/en-us/HT4790) hard drive encryption is so important.

Along with being able to share files and words, we need to be able to share secrets, aka passwords and logins. We use [1Password](https://agilebits.com/onepassword), available for free as a 30-day trial followed by a $50 purchase (check with your supervisor to see if we have any existing licenses you can use before submitting a purchase request). There is a keychain file shared via dropbox that contains a number of shared logins. See [this guide](https://support.1password.com/guides/mac/share-a-vault.html) on how to set that up.

## Other Guides

* [How to Setup Your Mac to Develop News Applications Like We Do](http://blog.apps.npr.org/2013/06/06/how-to-setup-a-developers-environment.html) on NPR Apps' blog
