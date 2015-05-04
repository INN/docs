# Releasing software

Preparing a repository for a new release:

- [ ] All must-have issues are closed (likely all normal and high priority issues).

- [ ] Move any left-over issues to the backlog or the next release as appropriate.

- [ ] Make sure a previous version tag exists.

        > git checkout master
        > git tag
        0.1
        0.2

        > git tag -a v0.3 -m "tagging v0.3"
    
        > git tag
        0.1
        0.2
        0.3

- [ ] Minify/compress assets (LESS/CSS, Javascript)

For example, to compile CSS and JS files in Largo:

    > git checkout develop
    > grunt less
    > grunt cssmin
    > grunt uglify

- [ ] Compile translation file(s).

For example, to compile translation files in Largo:

    > git checkout develop
    > grunt pot
    > msgmerge -o lang/es_ES.po.merged lang/es_ES.po lang/largo.pot
    > mv lang/es_ES.po.merged lang/es_ES.po

- [ ] Update the project's readme

For example, in Largo, make sure version numbers are update (see the next list item) and any links to Travs or Read The Docs are using the appropriate branch.

- [ ] Update the version number in the project

    - For Largo, update the version number in:
        - `style.css`
        - `readme.md`
        - `package.json`
        - `docs/conf.py`

- [ ] Run the test suite one last time to make sure you're not tagging a broken version

- [ ] Rebuild documentation

For example, to rebuild the PHP documentation in Largo

        > git checkout develop
        > grunt shell

- [ ] Merge develop branch into master and push

        > git checkout master
        > git merge develop
        > git push origin master

- [ ] Tag the new release

        > git tag -a v0.4 -m "tagging v0.4"

- [ ] Push newly created tags

        > git push origin --tags
