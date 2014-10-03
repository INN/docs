# INN's Best Practices

Based on [NPR Visuals' Best Practices](https://github.com/nprapps/bestpractices) with additions for WordPress and PHP.

The contents of this repository are released under a [Creative Commons CC BY 3.0 License](http://creativecommons.org/licenses/by/3.0/deed.en_US).

**Note:** This document references our fork of NPR's [app-template](http://github.com/INN/app-template) in several places and generally assumes you are using it.


## Index

* [Project documentation](#project-documentation)
* [Naming things](#naming-things)
* [Version control](#version-control)
* [Servers](#servers)
* [HTML and CSS](#html-and-css)
* [Javascript](#javascript)
* [Python](#python)
* [PHP](#php)
* [WordPress](#wordpress)
* [Assets](#assets)


## Project documentation

Always ensure the following things are documented in the README:

* Steps to setup the project from a blank slate. (Data loading, etc.)
* Required environment variables. If these are secrets they should stored in the team's secrets repo.
* Cron jobs that must be installed on the servers. When using the app-template specifying these in the `crontab` file is sufficient.
* Dependencies that are not part of our standard stack. This includes documenting how to install them. Whenever feasible this documentation should be in the form of `fab` commands.


## Naming things

Naming things (variables, files, classes, etc.) consistently and intuitively is one of the hardest problems in computer science. To make it easier, follow these conventions:

* Always proceed from more general to more specific. For example, ``widget-skinny`` is better than ``skinny-widget``.
* Strive for parallelism. If you have a `begin()` function, then have an `end()` function (not `stop()` or `done()`).
* Group related names with common prefixes, e.g. `search_query` and `search_address`.
* Prefer more specific terms to vague ones. If it's an address call it `address`, not `location`.
* When a function operates on a variable, the naming should be consistent. If working with `updates` then `process_updates()`, don't `process_changes()`. 
* Maintain naming conventions between lists and their iterators: `for update in updates`, not `for record in updates`.

<table>
  <tr><th>Prefer...</th><th>to...</th></tr>
  <tr><td>create</td><td>insert, add, new</td></tr>
  <tr><td>update</td><td>change, edit</td></tr>
  <tr><td>delete</td><td>remove, purge</td></tr>
  <tr><td>setup</td><td>init</td></tr>
  <tr><td>make</td><td>build, generate</td></tr>
  <tr><td>wrapper</td><td>wrap</td></tr>
  <tr><td>render</td><td>draw</td></tr>
</table>

(Note: sometimes these words don't mean the same thing, but when they do, prefer the former.)


## Version control

### The basics

* Development of major features should happen on separate branches which periodically merge *from* ``master`` until development of the feature is complete.
* A ``stable`` branch should always be present and should merge *from* ``master``, only when deploying to production.
* Don't store binary files (comps, databases) in the repository.
* If a binary object needs to be shared then store it in Dropbox or on S3. If it is part of the setup process (e.g., a database backup) then use fabric commands to read and write it.
* **Never, ever store passwords, keys or credentials in any repository.** (Use environment variables instead.)

### Where we host our code

We use Github and Bitbucket to host our code. 

-  Github is where we keep code meant for the general public. 
-  We use Bitbucket to house repositories that we deploy from. Code hosted on Bitbucket, while technically open, is usually member-specific. Typically, this is not code that anyone outside INN and its members will want to use or fork to start their own project but it is available and free to use should you find it helpful.

## Servers

* Environment variables belong in `/etc/environment`. This file should be sourced by cron jobs. (This happens automatically when using `run_on_server.sh`.)


## HTML and CSS

See [html_and_css.md](https://github.com/INN/docs/blob/master/style-guides/code/html_and_css.md).


## Javascript

See [javascript.md](https://github.com/INN/docs/blob/master/style-guides/code/javascript.md).


## Python

See [python.md](https://github.com/INN/docs/blob/master/style-guides/code/python.md).


## PHP

See [php.md](https://github.com/INN/docs/blob/master/style-guides/code/php.md).


## WordPress

See [wordpress.md](https://github.com/INN/docs/blob/master/style-guides/code/wordpress.md).


## Assets

See [assets.md](https://github.com/INN/docs/blob/master/style-guides/code/assets.md).