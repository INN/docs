# Installing SSL on sites

There are site-specific docs for each of these hosts:

- [WPEngine](./install-ssl-wpengine.md)
- [Flywheel](./install-ssl-flywheel.md)

Beyond that, here's a checklist of things to check that might need to be updated:

- [ ] Dashboard > Appearance > Theme Options > Theme Images: Update all URLs from `http:` to `https:`
- [ ] Dashboard > Settings > General > WordPress Address
- [ ] Dashboard > Settings > General > Site Address
- [ ] Search `/?s=pym` and update any Pym.js embed URLs
- [ ] follow troubleshooting options at https://getflywheel.com/wordpress-support/i-forced-ssl-and-now-my-images-arent-displaying/
