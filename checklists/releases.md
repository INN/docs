# Releasing software

## In general

Preparing a repository for a new release:

- [ ] All must-have issues are closed (likely all normal and high priority issues).

- [ ] Move any left-over issues to the backlog or the next release as appropriate.

- [ ] Prepare a changelog based on the issues and pull requests closed for the respective milestone/version number.

## Largo releases

This assumes all changes for a given release are included in the `develop` branch. This process works based on the assumption that releases are packaged by merging `develop` into the `master` branch.

- [ ] On the `develop` branch, update the version number in the project's `package.json` file.

- [ ] Run the `grunt build-release` task to build all assets, project documentation, language files and increment the version number in all appropriate files.

- [ ] Run the test suite one last time to make sure nothing is broken.

- [ ] Commit any changes.

For example:

    > git commit -m "running 'grunt build-release' ahead of v0.5.3 release"

- [ ] Run the `grunt publish` task to:
    - Checkout the `master` branch
    - Merge `develop` to `master`
    - Tag the release
    - Finally, push to the remote repository.

## After pushing a tagged release:

- [ ] Publish a `changelog` for the new version on the project page

## WordPress.org plugin directory releases

Refer to the [wordpress.org plugin directory about page](https://wordpress.org/plugins/about/) for information on procuring an svn repository.

Make sure the plugin has a readme.txt that:
- [ ] Conforms to the [WordPress readme standard](https://wordpress.org/plugins/about/readme.txt) and [validates](https://wordpress.org/plugins/about/validator/)
- [ ] Has the correct header information including our wp.org username (inn_nerds), donate link (inn.org/donate) and appropriate tags (see the list of popular wp.org tags here: https://wordpress.org/plugins/tags/)

Use this [release.sh](https://gist.github.com/rnagle/40d84cbd5fef86e3de7781fc31b46d94) gist as the base script for deploying plugins to a wordpress.org svn repository.

### Pre-release checklist:

- [ ] Update version numbers in all appropriate files
- [ ] Compile, minify, build, etc. all assets and language files
- [ ] Where applicable, run the test suite and fix any failing tests
- [ ] Commit all changes to master and push
- [ ] Tag a release (e.g., `git tag -a v0.4.0 -m "tagging v0.4.0"`)
- [ ] Push tags (e.g., `git push --tags`)

### Using the release.sh script

1. Copy the contents of [this gist](https://gist.github.com/rnagle/40d84cbd5fef86e3de7781fc31b46d94) to a `release.sh` file in the root of the plugin repository to be deployed/published.
2. Change the slug in the `release.sh` file from "plugin-slug-goes-here" to whatever the slug is for your plugin on wordpress.org.
3. Release/publish to wordpress.org: `./release.sh`. The first time you run this, you'll be asked to provide credentials for the svn repository.

NOTE: you can also test the release by running `./release.sh --dry_run`. This will produce a `release/wp-release.zip` file, the contents of which represent what will be published to wordpress.org.
