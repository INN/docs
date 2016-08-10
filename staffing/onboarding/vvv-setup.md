# Vagrant Setup Instructions

## Install VirtualBox, Vagrant, and VVV 

- Start by following the [official installation guide for VVV on Github[(https://github.com/varying-vagrant-vagrants/vvv/#installation---the-first-vagrant-up), but pay special attention to the notes below:
 - We strongly recommend also installing all of the optional Vagrant plugins mentioned in step 4. These will only make it easier and more convenient for you to use VVV later.
 - Between steps 6 and 7, you'll want to run the follwing commands to get the latest official release (without these you'll get the latest development build)

```
git fetch
git checkout master
```

## Install VV

Variable VVV (a.k.a. VV) provides some handy tools for building sites using VVV.

- Follow the installation [instructions found on GitHub](https://github.com/bradp/vv#os-x-installation). 

## Increase the Server Memory on Your Vagrant Box

- Use the command line to navigate to the root directory of your Vagrant box (where your Vagrantfile is located).
- Paste the following command into your terminal, hit Enter, and then type Control-D.

```
cat > Customfile
config.vm.provider "virtualbox" do |v|
  v.memory = 2048
  v.cpus = 4
end
```

- That created a new file, `Customfile` which increases the memory limit on your Vagrant box, as [recommended in the VVV documentation](https://github.com/Varying-Vagrant-Vagrants/VVV/wiki/Customising-your-Vagrant's-attributes-and-parameters).

## Setup a Largo Blueprint for VV

One useful feature of VV is that it allows you to create "blueprints" for site configurations. Below, we'll setup a basic blueprint for Largo sites.

- Paste the following command into your terminal, hit Enter, and then type Control-D.

```
cat > vv-blueprints.json
{
  "largo": {
    "themes": [
      {
        "location": "INN/largo",
        "activate": true
      }
    ],
    "options": [
      "current_theme::largo"
    ],
    "defines": [
      "WP_CACHE::false"
    ]
  }
}
```

- Alternatively, if you'd like to learn more about VV Blueprints and how they work, you can run `vv --blueprint-init` from the vagrant folder in your terminal to create a sample blueprint named `vv-blueprints.json`, which you'll modify to match the file above.

## Vagrant Up

- Now you're ready to run `Vagrant Up` and get started developing! Be patient, this can take ~10 minutes or so the first time you run it.

---

## Creating New Sites

By default, VVV gives you a few places to work from:

| URL                                   | Usage                                                         |
| ---                                   |---                                                            |
| http://local.wordpress.dev/           | for WordPress stable                                          |
| http://local.wordpress-trunk.dev/     | for WordPress trunk                                           |
| http://src.wordpress-develop.dev/     | for trunk WordPress development files                         |
| http://build.wordpress-develop.dev/   | for the version of those development files built with Grunt   |
| http://vvv.dev/                       | for a default dashboard containing several useful tools       |

You can create new environments easily using VV's site wizard by running `vv create` in the root folder of VVV.

To create a site with the Largo theme pre-installed and activated, enter `largo` as your blueprint name when prompted (to use the blueprint we created earlier).

If you want to explore more of what VV can do, just type `vv` into the terminal and you'll get a list of commands it accepts.
