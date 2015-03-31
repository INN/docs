# Best Practices for WordPress

### Baseline

Refer to our [best practices for PHP](/style-guides/code/php.md) as the baseline for working with WordPress.

- Get familiar with the WordPress [Theme Development](http://codex.wordpress.org/Theme_Development) documentation and their [Coding Standards](https://make.wordpress.org/core/handbook/coding-standards/) and [Inline Documentation Standards](https://make.wordpress.org/core/handbook/inline-documentation-standards/). Read [our specific requirements for inline documentation](/style-guides/code/wordpress.md#inline-documentation) below.
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

#### Inline Documentation

We believe that inline documentation of our WordPress-related code is important and necessary, both to help future developers (including our future selves) and to encourage less experienced developers to work with our code. If you're not convinced, read [this blog post on inline documentation by John Jacob Jacoby](http://jaco.by/2012/06/04/inline-documentation/), a major contributor to WordPress and related projects.

##### What should be documented?

- [PHP Files](/style-guides/code/wordpress.md#php-files)
- [Functions and Class Methods](/style-guides/code/wordpress.md#functions-and-class-methods)
- [Classes](/style-guides/code/wordpress.md#classes)
- [Public Class Properties](/style-guides/code/wordpress.md#public-class-properties)
- [WordPress Actions and Filters](/style-guides/code/wordpress.md#actions-and-filters)

##### How should it be documented?

We follow the [WordPress ethos on inline documentation](https://make.wordpress.org/core/handbook/inline-documentation-standards/), which is known for its simultaneous extensibility and accessibility to newer programmers. In particular, we draw from the [WordPress standards for PHP documentation](https://make.wordpress.org/core/handbook/inline-documentation-standards/php-documentation-standards/) on some key points. For more specific information about formatting and how to phrase your language, please refer to the WordPress standards.

###### PHP Files

PHP Files should start with a DocBlock, just after the opening `<?php`, that give an overview of what is contained in the file, and should have the following format. ([WordPress standards](https://make.wordpress.org/core/handbook/inline-documentation-standards/php-documentation-standards/#6-file-headers))

```php
/**
 * Summary (no period for file headers)
 *
 * Description. (use period)
 *
 * @link URL
 * @since x.x.x (if available)
 *
 * @package Largo
 * @subpackage Component
 */
```

Examples:

- wp-includes/post.php of the WordPress 4.1 source code ([source](https://github.com/WordPress/WordPress/blob/4.1-branch/wp-includes/post.php#L2-L8))

```php
<?php
/**
 * Post functions and post utility function.
 *
 * @package WordPress
 * @subpackage Post
 * @since 1.5.0
 */
```

###### Functions and Class Methods

Functions and class methods should include a DocBlock preceding their definition of the following format. ([WordPress standards](https://make.wordpress.org/core/handbook/inline-documentation-standards/php-documentation-standards/#1-functions-and-class-methods))

```php
/**
 * Summary.
 *
 * Description.
 *
 * @since x.x.x
 * @access (for functions: only use if private)
 *
 * @see Function/method/class relied on
 * @link URL
 * @global type $varname Description.
 * @global type $varname Description.
 *
 * @param type $var Description.
 * @param type $var Optional. Description.
 * @return type Description.
 */
```

Examples:

- `get_post()` as defined in wp-includes/post.php of the WordPress 4.1 source code ([source](https://github.com/WordPress/WordPress/blob/4.1-branch/wp-includes/post.php#L402-L416))

```php
/**
 * Retrieves post data given a post ID or post object.
 *
 * See {@link sanitize_post()} for optional $filter values. Also, the parameter
 * $post, must be given as a variable, since it is passed by reference.
 *
 * @since 1.5.1
 *
 * @param int|WP_Post $post   Optional. Post ID or post object. Defaults to global $post.
 * @param string      $output Optional, default is Object. Accepts OBJECT, ARRAY_A, or ARRAY_N.
 *                            Default OBJECT.
 * @param string      $filter Optional. Type of filter to apply. Accepts 'raw', 'edit', 'db',
 *                            or 'display'. Default 'raw'.
 * @return WP_Post|null WP_Post on success or null on failure.
 */
function get_post( $post = null, $output = OBJECT, $filter = 'raw' ) {
```

###### Classes

Classes should include a DocBlock immediately preceding their declaration with a summary of their purpose. (Although the WordPress standard specifies that these should be documented, there is no specification in the WordPress standards. The implementation in the WordPress source code is also spotty.)

```php
/**
 * Summary.
 *
 * Description.
 *
 * @package Largo
 * @subpackage Component
 * @since x.x.x
 */
```

Examples:

- `WP_Post` class defined in wp-includes/post.php of the WordPress 4.1 source code ([source](https://github.com/WordPress/WordPress/blob/4.1-branch/wp-includes/post.php#L449-L454))

```php
/**
 * WordPress Post class.
 *
 * @since 3.5.0
 *
 */
final class WP_Post {
```

- `WP_Http` class defined in wp-includes/class-http.php of the WordPress 4.1 source code ([source](https://github.com/WordPress/WordPress/blob/4.1-branch/wp-includes/class-http.php#L15-L27))

```php
/**
 * WordPress HTTP Class for managing HTTP Transports and making HTTP requests.
 *
 * This class is used to consistently make outgoing HTTP requests easy for developers
 * while still being compatible with the many PHP configurations under which
 * WordPress runs.
 *
 * Debugging includes several actions, which pass different variables for debugging the HTTP API.
 *
 * @package WordPress
 * @subpackage HTTP
 * @since 2.7.0
 */
class WP_Http {
```

###### Public Class Properties

Each public property of a class should include a DocBlock before it that summarizes its purpose and indicates its type. We deviate from the WordPress Way here in that we do not require documentation of non-public class properties. ([WordPress standards](https://make.wordpress.org/core/handbook/inline-documentation-standards/php-documentation-standards/#2-class-properties))

```php
/**
 * Summary.
 *
 * @since x.x.x
 * @var type $var Description.
 */
```

Examples:

- `post_author` property of the `WP_Post` class defined in wp-includes/post.php of the WordPress 4.1 source code ([source](https://github.com/WordPress/WordPress/blob/4.1-branch/wp-includes/post.php#L464-L470))

```php
/**
 * ID of post author.
 *
 * A numeric string, for compatibility reasons.
 *
 * @var string
 */
public $post_author = 0;
```

###### Actions and Filters

Actions and filters should include a DocBlock immediately preceding the call to `do_action()` or `apply_filters()` with the following format. ([WordPress standards](https://make.wordpress.org/core/handbook/inline-documentation-standards/php-documentation-standards/#4-hooks-actions-and-filters))

```php
/**
 * Summary.
 *
 * Description.
 *
 * @since x.x.x
 *
 * @param type  $var Description.
 * @param array $args {
 *     Short description about this hash.
 *
 *     @type type $var Description.
 *     @type type $var Description.
 * }
 * @param type  $var Description.
 */
```

Examples:

- `do_action( 'registered_post_type', $post_type, $args )` in wp-includes/post.php of the WordPress 4.1 source code ([source](https://github.com/WordPress/WordPress/blob/4.1-branch/wp-includes/post.php#L1455-L1462))

```php
/**
 * Fires after a post type is registered.
 *
 * @since 3.3.0
 *
 * @param string $post_type Post type.
 * @param object $args      Arguments used to register the post type.
 */
do_action( 'registered_post_type', $post_type, $args );
```

- `apply_filters( "post_type_labels_{$post_type}", $labels )` in wp-includes/post.php of the WordPress 4.1 source code ([source](https://github.com/WordPress/WordPress/blob/4.1-branch/wp-includes/post.php#L1455-L1462))

```php
/**
 * Filter the labels of a specific post type.
 *
 * The dynamic portion of the hook name, `$post_type`, refers to
 * the post type slug.
 *
 * @since 3.5.0
 *
 * @see get_post_type_labels() for the full list of labels.
 *
 * @param array $labels Array of labels for the given post type.
 */
return apply_filters( "post_type_labels_{$post_type}", $labels );
```

##### Notes

- For each type of DocBlock, refer to the WordPress documentation on how each tag (e.g. `@param`) should be used. If it's still unclear, refer to the [WordPress reference on PHPDoc Tags](https://make.wordpress.org/core/handbook/inline-documentation-standards/php-documentation-standards/#phpdoc-tags).

- For the tags `@since` and `@deprecated`, be sure that these accurately reflect the project's version at the time the feature was added or deprecated.

- When using the `@package` tag, be sure to use the name of the containing project. If working on Largo, this should be `@package Largo`.

- When creating multi-line comments in the code that are not meant to be seen in the extracted PHP documentation, be sure to **not** start your block with `/**` and instead with a single asterisk `/*`.

**GOOD**:

```php
/*
 * This is a comment that is long enough to warrant being stretched over
 * the span of multiple lines. You'll notice this follows basically
 * the same format as the PHPDoc wrapping and comment block style.
 */
```

**BAD**:

```php
/**
 * This multi-line comment will appear in the extracted PHP documentation
 * and may not make sense in context. Use with caution.
 */
```
