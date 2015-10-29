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
