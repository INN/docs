# Client Hosting Manager

Status: &#128128; retired

## Relevant links:

- GitHub repo: https://github.com/inn/client-hosting-manager
- Wordpress.org plugin repo: https://wordpress.org/plugins/client-hosting-manager/
- Instructions on removal: https://github.com/INN/umbrella-currentorg/issues/17

## What is it?

Once upon a time, many INN member sites were all hosted as part of a single multisite WordPress install. And many users on those sites had admin access. WordPress single-site admins could still update plugins, but we didn't want them to be able to do that, because it would affect sites other than their own. Thus, we needed to selectively remove certain permissions from users who were not INN staff, which are documented [in the plugin's readme](https://github.com/INN/client-hosting-manager/blob/master/README.md)

Users of this plugin would need to define several constants which would determine which users were allowed to have which permissions by matching those users' email address domains.

If the plugin were removed from a site without first deactivating it while the constants were set, the plugin's permissions changes would remain permanently. The problems can be fixed with [`wp cap`](https://developer.wordpress.org/cli/commands/cap/).

## Who made it?

RC Lations, Ben Keith
