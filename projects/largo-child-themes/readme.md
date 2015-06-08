# Starting New Largo Child Themes

WordPress Child Themes inherit the files, functions, script and style of their Parent Theme.

Largo is structured a specific way, and when you create a child theme it will be easiest for you to follow parallel structures as you modify and add.

### Largo Child Theme Structure

![Visual Representation of Child Theme Structure](https://raw.githubusercontent.com/INN/docs/master/projects/largo-child-themes/structure.jpg)

### Sample Gruntfile

Look at ```Gruntfile.js``` here in the Largo Sample Child Theme.

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
-

### Other Largo Child Theme Resources
- [Child Themes Checklist](https://github.com/INN/docs/blob/master/checklists/updating-child-themes.md) in INN/docs.
- [Largo Documentation --> For Developers](http://largo.readthedocs.org/developers/fordevelopers.html#overview) on readthedocs.org.
- [Largo Sample Child Theme](https://github.com/INN/Largo-Sample-Child-Theme) in INN/Largo-Sample-Child-Theme
