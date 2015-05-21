Research:

- [ ] What plugins are used by the site?
- [ ] What is the current version of Largo? What version was this child theme built for? [What has changed since then?](https://github.com/INN/Largo/releases)
- [ ] Is the site already using the LESS customizer?
- [ ] Does the theme include many custom functions? What do they do?
- [ ] Document requirements in the theme's README.md.

Cleanup:

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

Checking

- [ ] Make sure that the site loads without errors on Vagrant
- [ ] Do the widgets look okay?
- [ ] What about these locations?
 	- [ ] Homepage
 	- [ ] Articles
 	- [ ] Series
 	- [ ] Category archive pages
 	- [ ] Series landing pages
 	- [ ] Search pages
 	- [ ] Tag archives
