# Starting New Largo Child Themes

WordPress Child Themes inherit the files, functions, script and style of their Parent Theme.

Largo is structured a specific way, and when you create a child theme it will be easiest for you to follow parallel structures as you modify and add.

### Largo Child Theme Structure

![Visual Representation of Child Theme Structure](https://raw.githubusercontent.com/INN/docs/master/projects/largo-child-themes/structure.jpg)

#### ```/less```

Standard File Names
- ```style.less``` - @import all other LESS here (use order here). This file generates style.css in ```css/style.css```.
- ```variables.less``` - Define Brand and Theme Colors Here, as well as @sans, @serif and @headline fonts.
- ```_global.less``` - Define major elements like body, anchors, buttons and other global styles here.
- ```_header.less``` - Define Site Header, Global Navigation, and Main Navigation styles here. Use these sections to organize the file.
- ```_single.less``` - Define styles for the Article Header, Article Body, Article Footer and Below Article here. Use these sections to organize the file.
- ```_archives.less``` - Define styles for Author Pages, Category Archives, Time-Based Archives, Series and Custom Taxonomies here. Use these sections to organize the file.
- ```_footer.less``` - Define Site Footer styles here.
- ```_plugin-slug.less``` - Define plugin-specific style here, including but not limited to Plugin Widgets, Pages, etc.

#### ```/css```

- ```style.css``` - An unminified version of ```less/style.less``` processed into CSS. You might need to create a blank file first time around.
- ```style.min.css``` - Minified version of ```css/style.css`` used in production. You might need to create a blank file first time around.

### Sample Gruntfile

Look at ```Gruntfile.js``` [here](https://github.com/INN/Largo-Sample-Child-Theme/blob/master/Gruntfile.js) in the Largo Sample Child Theme.

###Override Largo Template Parts and Add Custom Parts

To override a template part from Largo:
1. Create a ```/partials``` directory in your child theme.
2. Copy the partial over from Largo you plan to modify, preserving the filename.
3. Make your changes.

This uses the get_template_part WordPress function. The only difference is that Largo stores template parts in a partials directory.

As you build custom elements, you can and should store these theme parts in this directory.

###Override Largo Custom Functions

To override a custom function from Largo (like the byline output):
1. Create a ```/inc``` directory in your child theme.
2. Copy the file containing the custom function over from Largo you plan to modify, preserving the filename.
3. Make your changes.

### Development Guidelines
- **Don't move functions to a new location.** Overriding largo_byline() output? It should be in ```/inc/post-meta.php```, not ```functions.php```.
- **Don't Rebuild the Wheel**. Always modify and use existing functions instead of DIY. This saves clients money, us time and future us hassle.
- **Don't assume the plugin is there**. Wrap plugin-dependent functions with ```if(function_exists('function')){ plugin_dependent_function(); }``` to prevent missing plugins from breaking the site.

### Other Largo Child Theme Resources
- [Child Themes Checklist](https://github.com/INN/docs/blob/master/checklists/updating-child-themes.md) in INN/docs.
- [Largo Documentation --> For Developers](http://largo.readthedocs.org/developers/fordevelopers.html#overview) on readthedocs.org.
- [Largo Sample Child Theme](https://github.com/INN/Largo-Sample-Child-Theme) in INN/Largo-Sample-Child-Theme
