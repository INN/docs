# Write the docs!

Here you'll find our plans for the OpenNews Code Convening at Write the Docs, May 17, 2015.

Cheers to making [Largo's](https://github.com/INN/Largo) documentation great!

## Our audience:

Our primary audience for the work we aim to complete this weekend is the group of developers using Largo as the base/parent theme for their news site. We want to pay special attention to the INN's members that are short on time, money and technical skill.

## Our goals:

- We're aiming to start filling out the API docs/function reference, which means LOTS of cleanup of Largo source code.
- We need technical docs for those people looking to use Largo as a framework to customize and/or enhance their site.
	- Homepage layout system.
	- Child themes (partially covered in Largo Sample Child Theme).
	- Custom Largo functionality that can be used in widgets and child theme.
	- How to setup a development environment to work on your child theme.
	- Teach people how to work with us more effectively.

## Assumptions:

- Our audience has some background in programming. They are familiar with the high-level components of computer programming (e.g., variables, functions, conditions, etc.).
- Our audience may not be familiar with PHP, WordPress or Largo. We should use plain language and be as explicit as possible in order to help them reach their goal. 

## Resources for potential contributors:

Our docs are written using reStructuredText:

- [Sphinx tipsheet on rST](http://sphinx-doc.org/rest.html)
- [rST quick reference](http://docutils.sourceforge.net/docs/user/rst/quickref.html)

Our API docs/function reference are embedded in Largo's source code. This portion of the documentation uses an intermediate processing layer that extracts the documentation from the source code and creates reStructuredText files that Sphinx can understand and render.

- [INN's doc for writing inline documentation](https://github.com/INN/docs/blob/master/style-guides/code/wordpress.md#inline-documentation)
    - This doc is aspirational and may not work 100% with the strategy we're using to document our source code. We're OK with that, for now.
- [The current state of the docs](https://largo.readthedocs.org/en/write-the-docs/api/)
- ["Write the Docs" milestone on Github](https://github.com/INN/Largo/milestones/Write%20The%20Docs)

### Getting started

1. [Fork INN/Largo](https://github.com/INN/Largo#fork-destination-box)
2. Clone your branch:


	    git clone git@github.com:you/Largo.git

3. Check out the `write-the-docs` branch:


    	git checkout write-the-docs

4. Install dependencies:

We use some Python libraries to generate our documentation. To install the requirements:

    	cd docs

Not required, but it's recommended to use virtualenv:

    	mkvirtualenv largo-docs
    	workon largo-docs
Then:

    	pip install -r requirements.txt

5. Our API docs/function reference uses doxphp to generate documentation based on the comments embedded in Largo's source code. You'll need to install doxphp to generate API docs.

    - Install with PEAR:

            pear channel-discover pear.avalanche123.com
            pear install avalanche123/doxphp-beta


6. With all dependencies installed, running the generator is as simple as:


    	cd docs
    	make php && make html


7. You can view the generated docs in the `docs/_build/html` directory.
    - You can view the files with a browser as files
    - You can run a simple web server to view them.

        	cd docs/_build/html
            python -m SimpleHTTPServer 8081


    - Open a browser and point it at http://localhost:8081

### The (ideal) procedure for contributing

1. [Choose an issue](https://github.com/INN/Largo/milestones/Write%20The%20Docs)
2. Comment on the issue that you're taking it.
3. Create a new branch with your contributions, named after the issue:

        git checkout -b 613-partials-sticky-posts

4. Make your changes
5. Commit and push:

        git commit
        git push -u origin 613-partials-sticky-posts

6. Create a pull request from your branch against INN/Largo, branch write-the-docs
    - How to make a [PR on GitHub](https://help.github.com/articles/creating-a-pull-request/)
    - If it's a big PR, please [make sure it's well-documented](/how-to-work-with-us/pull-requests.md). Thanks!
7. Done? Return to step 3.
