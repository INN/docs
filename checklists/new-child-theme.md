## Repo setup

- [ ] Create a new repository on Bitbucket under the `projectlargo` account.
	- Don't create it with any new files, readme, or license file. You want it to be blank.

On your machine, in a new directory, create a style.css file:

- [ ] theme style.css with [appropriate metadata](https://codex.wordpress.org/Theme_Development#Theme_Stylesheet).
	- The best way to do this is [find an existing child theme](https://bitbucket.org/projectlargo/) and copy from there.

Then, initialize git and add the new Bitbucket repository as a remote, according to the instructions Bitbucket gave you.

```
git init
git remote add origin <url>
git add style.css
git commit -m "Initial commit"
git push -u origin master
```

## Adding it to umbrella

In the umbrella:

```
cd wp-content/themes/
git submodule add <repo url> <repo name>
git submodule update --init --recursive
git commit -m "added new child theme"
```

## Adding files

- [ ] theme functions.php
	- If the theme doesn't have any custom functionality (rare) you don't need to create this. It will be created later.
	- Remember to Follow our [formatting guidelines](https://github.com/INN/docs/blob/master/style-guides/code/php.md) and [document your code](https://en.wikipedia.org/wiki/PHPDoc)
- [ ] Gruntfile.js and the `less` and `css` dirs

### Custom homepages

tk: make sure that the docs here are thorough and explain lots of things

- [ ] template
- [ ] layout
- [ ] zones
- [ ] assets (amd make sure to add them to the Grunt file)

Places to improve docs:
- zones
- the zone/template relationship as mediated by the layout
