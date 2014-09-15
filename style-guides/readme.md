# Code quality and style guide

*This is my code quality and best practices guide. There are many like it, but this one is mine.*

## General style and formatting of code:

1. Readability is king.
2. Consistency is important.

Here are some ways to keep your code readable and consistent when working collaboratively:

### Basic text editor set up:

- Use four space, soft tabs when editing Python.
- Use two space, soft tabs when editing HTML, CSS, and Javascript.
- Maximum line length should not exceed 100 characters

### Style guide for PHP and WordPress

- Embrace convention and use hard tabs when [working with WordPress](http://make.wordpress.org/core/handbook/coding-standards/php/#indentation).
- When something goes wrong, throw an Exception.
- Return values for a group of related or similar functions should be consistent and predictable.
    - For example, don't alternate between return values of null and '' and false when an error occurs. If you decide it's really not appropriate to throw an Exception, be consistent in the value your function returns.
- Favor the use of WordPress' database model classes (i.e. WP_* classes) to convenience methods like get_user or `wp_insert_user`.
- Keep your variables and object attribute names consistent with the existing WordPress schema. In other words, if the `WP_User` attribute is `user_login`, don't name your variable `userLogin` or `user_name` — stick with `user_login`.
- Work with, not against, The Loop.
- Keep the use of third party PHP libraries to a minimum. Chances are good that your third party lib will need to be refactored if you plan on submitting a theme or plugin to WordPress.

## Other guiding principles:

- I'll say it again: readability is king. If reading your code induces pain, I will find you.
- When interacting with external APIs, keep the number of backend requests to a minimum, especially if said request are made while your user is waiting.
- Embrace the [Zen of Python](http://legacy.python.org/dev/peps/pep-0020/), no matter what program language you're using.

## Other resources:

- Review [Python's PEP8](http://legacy.python.org/dev/peps/pep-0008/) for lots of good tips regarding readability. Much of PEP8 can be applied to languages other than Python. Use your best judgment.
- See [NPR Visuals' Best Pratices](https://github.com/nprapps/bestpractices).
