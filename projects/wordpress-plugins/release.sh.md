## Working with release.sh

Many of our plugins use a shell script, `release.sh`, to handle pushing new versions to `wordpress.org`'s plugins SVN repository.

This file provides setup, usage, and configuration instructions for `release.sh`.

### The first release

1. Review the files in the `WHITELIST` and `BLACKLIST` variables in `release.sh`. Make changes as necessary.
2. Update the `SVN_REPO` variable with your plugin's `plugins.svn.wordpress.org` SVN repository.
3. `chmod +x release.sh`
4. Add `release/` to the project's `.gitignore`
5. Commit all changes and push your commits to the plugin's repository.
6. Run `release.sh`.
  - You may need to verify the receiving server's key fingerprint.
  - If it asks you to enter the password for your computer's username, press the `[enter]` key to get the username prompt, then enter your `wordpress.org` username and password.

### Later releases

1. Run `release.sh`

### Plugins using `release.sh`

This list may be incomplete.

- The original script: https://github.com/publicmediaplatform/pmp-wordpress/blob/master/release.sh
- https://github.com/INN/DoubleClick-for-WordPress
- https://github.com/INN/link-roundups
- https://github.com/INN/super-cool-ad-inserter-plugin

Significant changes to `release.sh` should be copied between plugins.
