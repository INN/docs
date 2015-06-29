### Research:

- [ ] What plugins are used by the site?
- [ ] What is the current version of Largo? What version was this child theme built for? [What has changed since then?](https://github.com/INN/Largo/releases)
- [ ] Is the site already using the LESS customizer?
- [ ] Does the theme include many custom functions? What do they do?
- [ ] Does the theme include any custom partials or templates? What do they override? Can they be removed?
- [ ] Document requirements in the theme's README.md.

### Cleanup:

- [ ] Go through theme, file-by-file, and check for
	- Child theme code duplicating Largo code
	- Child theme code that is outdated
	- Functions that depend upon plugins
- [ ] Wrap plugin-dependent functions in `if(function_exists('function')){ function(); }` to prevent missing plugins from breaking the site.
- [ ] Remove child theme code that is exact duplicate of Largo code
- [ ] Remove child partials that are exact duplicate of Largo partials
- [ ] Remove Helvetica from font families.
- [ ] For inexact duplicates, see if there is a hook or filter that can be used to the same effect
- [ ] Consider using Largo's LESS customizer for changing main colors
- [ ] Document requirements in the theme's README.md

Then, and only then, should you switch the line in the child theme's `style.css` from `Template: largo` to `Template: largo-dev`.

### Enabling the new theme

For the site (on Vagrant, on staging, and on production), you'll need to:

- Enable the current Largo theme version >=v0.4 in Sites > Themes > Project Largo (by The INN Nerds) > Enable
- In Appearance > Themes, temporarily switch to the newest version of Project Largo - Base Theme
- Switch to the updated child theme. 
- Run the Largo Update if prompted in the admin interface.

This procedure is needed to reset WordPress' knowledge of the child theme's parent, which is only updated on theme activation.

### Checking

- [ ] Make sure that the site loads without PHP errors on Vagrant
- [ ] Do the widgets look okay?
- [ ] Are the menus okay?
- [ ] What about these locations? `common url`
 	- [ ] Homepage `/`
 	- [ ] Articles `/?p=1234`
 	- [ ] Series `/series/slug/` `/?series=1234`
 	- [ ] Category archive pages `/category/slug/`
 	- [ ] Series archive pages `/series/slug/`
 	- [ ] Series landing pages `/slug/`
 	- [ ] Search results `/?s=words`
 	- [ ] Pages `/slug/`
 	- [ ] Tag archives `/tag/slug`
