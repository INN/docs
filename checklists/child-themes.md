# Child Theme Review

A checklist for reviewing child themes when updating from an earlier version of Largo. Also a general checklist for doing a theme review for any child themes we didn't build before allowing them on our hosting.

### Research

- [ ] What plugins are used by the site?
- [ ] What is the current version of Largo? What version was this child theme built for? [What has changed since then?](https://github.com/INN/Largo/releases)
- [ ] Is the site already using the LESS customizer?
- [ ] Does the theme include any custom functions? What do they do?
- [ ] Does the theme include any custom partials or templates? What do they override? Can they be removed?
- [ ] If the custom partials and templates cannot be removed, are they loaded by the Load More Posts button? If they are not, the theme needs a function to choose the correct partial for the [`largo_lmp_template_partial` filter in `largo_load_more_posts_choose_partial`](https://github.com/INN/Largo/blob/master/inc/ajax-functions.php#L192). Example code for the filter can be seen in [this theme's functions.php](https://bitbucket.org/projectlargo/theme-aspen/src/master/functions.php?at=master).
- [ ] Document requirements in the theme's README.md


### Cleanup

- [ ] Run the [theme check plugin](https://wordpress.org/plugins/theme-check/) and fix any warnings that appear
- [ ] Go through theme, file-by-file, and check for
	- Child theme code duplicating Largo code
		- Redefined `largo_load_more_posts` will have been broken by [0.5.1](https://github.com/INN/Largo/releases/tag/v0.5.1), and will need to be updated based on [the current code](https://github.com/INN/Largo/blob/master/inc/ajax-functions.php#L70)
	- Child theme code that is outdated
	- Functions that depend upon plugins
- [ ] Make sure the child theme structure matches that of our [sample child theme](https://github.com/INN/Largo-Sample-Child-Theme) and all code follows our [coding standards](/style-guides/code)
- [ ] Wrap plugin-dependent functions in `if(function_exists('function')){ function(); }` to prevent missing plugins from breaking the site.
- [ ] Remove child theme code that is exact duplicate of Largo code and any partials that are exact duplicate of Largo partials
- [ ] Note any examples of code that is likely to cause us problems with future updates, consider reverting to default partials, code, behavior wherever possible. Exceptions should have a clear reason for being and we should ask members/clients to provide justification for anything questionable and reserve the right to say no.
- [ ] [Rename style.css to child-style.css](https://github.com/INN/Largo-Sample-Child-Theme/issues/14)
- [ ] For inexact duplicates, see if there is a hook or filter that can be used to the same effect
- [ ] Consider using Largo's LESS customizer for changing main colors
- [ ] Any pertinent information should be included in the child theme's readme

Then, and only then, should you switch the line in the child theme's `style.css` from `Template: largo` to `Template: largo-dev`.


### Enabling a new child theme

Enabling a child theme can be a bit problematic, particularly if the template (parent theme) name has changed.

The following procedure is needed to reset WordPress' knowledge of the child theme's parent, which is only updated on theme activation. 

For the site (on Vagrant, on staging, and on production), you'll need to:

- Enable the current Largo theme version in Network Admin (assuming you're using WordPress multisite) > Sites > Themes > Project Largo (by The INN Nerds) > Enable
- Then, from the child site, in Appearance > Themes, temporarily switch to the current version of Project Largo - Base Theme
- Then, switch to the updated child theme (this should update the "Template" option in the wp_options table and make sure WordPress is using the correct version of the Largo parent theme)
- Run the Largo update if prompted to do so in the admin interface

Alternatively, if you're comfortable with editing the database directly, you can change the template name in the blog's wp_options table, or you can edit this option under Network Admin > Sites > [Your Child Theme] > Edit > Settings. Look for the option called "Template" and make sure it has been set to the name of the folder containing the latest version of the Largo parent theme.


### Testing

- [ ] Make sure that the site loads without PHP errors on Vagrant
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
- [ ] Load More Posts
	- [ ] Did you define a custom archive template?
	- [ ] Does the custom archive template load the correct partial when the Load More Posts button is clicked?
- [ ] Styles?
	- [ ] Sticky nav
		- [ ] Mobile
		- [ ] Desktop
	- [ ] Non-sticky nav
	- [ ] Widgets
	- [ ] Article
		- [ ] Social buttons
		- [ ] Type
		- [ ] Fonts rendered are fonts specified in stylesheet ( In Chrome: "Inspect element" on a `<p>`, then look at the bottom of the "Computed" tab. )
		- [ ] Images
	- [ ] Footer
