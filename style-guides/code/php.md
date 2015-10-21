# Best Practices for PHP

### Baseline

Follow the Wordpress [PHP Coding Standards](http://nerds.inn.org/2014/10/02/spaces-or-tabs-which-will-you-choose/)

- Use tabs instead of spaces
- Use { } even when they're not necessary:  

	if ( condition ) {
		action0();
	}

- Remove trailing spaces

One notable exception to WordPress' rules is that we do not use spaces or tabs for indentation within a line of code.

Other things:

- When something goes wrong, use an Exception.
- Use [namespaces](http://php.net/manual/en/language.namespaces.php).

### Documentation

INN's PHP projects use [phpDocumentor-style](http://manual.phpdoc.org/HTMLSmartyConverter/PHP/phpDocumentor/tutorial_phpDocumentor.quickstart.pkg.html#coding.phpcomments) documentation comments, [following the WordPress standard](https://make.wordpress.org/core/handbook/best-practices/inline-documentation-standards/php/).
