# Best Practices for WordPress

### Baseline

Refer to our [best practices for PHP](/style-guides/code/php.md) as the baseline for working with WordPress.

- Get familiar with the WordPress [Theme Development](http://codex.wordpress.org/Theme_Development) documentation and their [Coding Standards](http://codex.wordpress.org/WordPress_Coding_Standards).
- Embrace doing things The WordPress Way. Even if you disagree ([sometimes we do](http://nerds.inn.org/2014/10/02/spaces-or-tabs-which-will-you-choose/)). Your software will be easier to maintain as new versions of WordPress are released and easier for others to contribute to.
- In a fight, the WordPress Way wins.

### Specifics

- Use tabs when [working with WordPress](http://make.wordpress.org/core/handbook/coding-standards/php/#indentation).

- Return values for a group of related functions should be consistent and predictable.

    Given the hypothetical functions `create_user_profile`, `update_user_profile` and `destroy_user_profile`, each should:

    - Exhibit the same behavior when an error occurs. In other words, don't alternate between return values of null and '' and false. Return a `WP_Error` or throw an Exception.

    - Return something **sane** on success.

        For example, the function name `create_user_profile` gives a strong indication that it performs an action on a user profile. It would be **sane** to expect a UserProfile object or the ID of the user profile as a return value from this function.

- Keep your variables and object attribute names consistent with the existing WordPress schema.

    In other words, if the `WP_User` attribute is `user_login`, don't name your variable `userLogin` or `user_name` — stick with `user_login`.

    Do this and avoid having to map your variable names to WordPress' variable names.

- Work with, not against, [The Loop](http://codex.wordpress.org/The_Loop).

    This means taking advantage of the [template tags](http://codex.wordpress.org/Stepping_Into_Template_Tags#Template_Tags_and_The_Loop) that WordPress includes to make displaying content on your site easier. There are lots of convenience functions like `the_content()` that only work within the loop.

    Note: The Loop, along with many other parts of WordPress, uses global variables to track the application's state.

    Typically, using global variables is a [bad idea](http://programmers.stackexchange.com/a/148109). Try to avoid using them in your code, but be aware that many of the "magic" or "it just works" functions in WordPress are built using global variables.

    Another note: you can create your own Loop using [WP_Query](http://codex.wordpress.org/Class_Reference/WP_Query), which will allow you to ([almost](http://codex.wordpress.org/Function_Reference/wp_reset_postdata)) avoid using global variables.

- Keep the use of third party PHP libraries to a minimum.

    Chances are that your third party lib will need to be refactored if you plan on submitting a theme or plugin to WordPress.
