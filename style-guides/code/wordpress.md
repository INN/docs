## Best Practices for WordPress

### Baseline

Refer to our [best practices for PHP](https://github.com/INN/bestpractices/blob/master/php.md) as the baseline for working with WordPress.

### Specifics

- Embrace convention and use hard tabs when [working with WordPress](http://make.wordpress.org/core/handbook/coding-standards/php/#indentation).

- Return values for a group of related functions should be consistent and predictable.

    Given the hypothetical functions `create_user_profile`, `update_user_profile` and `destroy_user_profile`, each should:

    - Exhibit the same behavior when an error occurs. In other words, don't alternate between return values of null and '' and false. Return a `WP_Error` or throw an Exception.

    - Return something **sane** on success.

        For example, the function name `create_user_profile` gives a strong indication that it performs an action on a user profile. It would be **sane** expect a UserProfile object or the ID of the user profile as a return value from this function.

- Keep your variables and object attribute names consistent with the existing WordPress schema.

    In other words, if the `WP_User` attribute is `user_login`, don't name your variable `userLogin` or `user_name` — stick with `user_login`.

    Do this and avoid having to map your variable names to WordPress' variable names.

- Work with, not against, The Loop.

- Keep the use of third party PHP libraries to a minimum.

    Chances are that your third party lib will need to be refactored if you plan on submitting a theme or plugin to WordPress.
