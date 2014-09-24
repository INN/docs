## Best Practices for WordPress

### Baseline

Refer to our [best practices for PHP](https://github.com/INN/bestpractices/blob/master/php.md) as the baseline for working with WordPress.

### Specifics

- Embrace convention and use hard tabs when [working with WordPress](http://make.wordpress.org/core/handbook/coding-standards/php/#indentation).

- Return values for a group of related or similar functions should be consistent and predictable.

    For example, don't alternate between return values of null and '' and false when an error occurs. If you decide it's really not appropriate to throw an Exception, be consistent in the value your function returns.

- Keep your variables and object attribute names consistent with the existing WordPress schema.

    In other words, if the `WP_User` attribute is `user_login`, don't name your variable `userLogin` or `user_name` — stick with `user_login`.

- Work with, not against, The Loop.

- Keep the use of third party PHP libraries to a minimum.

    Chances are that your third party lib will need to be refactored if you plan on submitting a theme or plugin to WordPress.
