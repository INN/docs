# Exercises

### For a mid-level WP developer (mostly theme dev)

##### (Written for Religion News Service, October 2015)

This test is intended to test your general knowledge of WordPress concepts that are helpful for the development of child themes. For all of the below, please write code that conforms to the WordPress coding and documentation standards. The way you approach and work through these problems is as important (if not more important) than the solution you arrive at. Please be prepared to talk through your process, any obstacles you encountered, things you tried and how you arrived at your solution.

**Here are some resources you might find helpful:**

Largo documentation - [https://largo.readthedocs.org/](https://largo.readthedocs.org/)
Sample Largo child theme - [https://github.com/INN/Largo-Sample-Child-Theme](https://github.com/INN/Largo-Sample-Child-Theme)

**Setup:**

1. Using hosting of your choice (or you can just work locally), create a clean installation of WordPress.
2. Download and install the Largo theme from http://github.com/inn/largo.
3. Create and activate a new WordPress child theme that uses the Largo theme as its parent.

**Child theme modifications:**

1. Change the default link color throughout the site to #ffefd5. On hover it should change to #d5e5ff.
2. From the WordPress dashboard, create a category called “Test Category”. For posts in this category, we don’t want to automatically display featured images at the top of posts. Write code to hide the featured images on all posts in this category.
3. In your child theme, register a new widget area called “Test Widget Area”. This widget area should be displayed only on the category archive page for your Test Category and should contain only the Largo About and Largo Follow widgets. Write the necessary code to create the widget area, assign this default set of widgets and display it on the correct category archive page. 

**Wrap-up:**

1. Create a github repository for your child theme and push the results of this exercise (just the child theme folder).

**Additional questions:**

1. You are asked to add a plugin to the site to restrict access to a section of the site to only paid subscribers. Which plugin would you recommend? Discuss how you selected this plugin and any criteria you used for review.
2. Authors/editors would like to be able to preview their stories to see how they look on different devices/screen sizes. What tool(s) would you recommend?
