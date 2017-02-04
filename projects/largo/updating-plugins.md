# Plugins Update Process

This document describes a standard process for updating WordPress plugins for any sites we host. This process applies to both Staging and Production environments. For the sake of demonstration, we're using the largoproject install, but the process would be same for any site we have hosted on WP Engine. 

## Why

- WordPress plugins vary in quality, and updates can cause unforeseen problems.
- While we try to limit the number of plugins used on any given site and avoid making exceptions to our list of recommended plugins, some sites have plugins that are known to trigger bad behavior after an update.
- We want to avoid disrupting member sites after an update.

## Timing

The timing of the updates should avoid times when Largo sites are most frequently publishing and updating content, ideally in the evening or over the weekend. If we have to restore, this should minimize wiping out content entered after the backup point. 

Also, allow for one hour of work time per instance (staging and production) after installing the plugin updates for testing and addressing any problems. Staging should be updated first and tested, closely followed by production. We want the conditions to be as identical as possible between staging and production when the updates are applied. Where possible, production should be cloned to staging before testing.

**DO NOT** perform updates or deploy any significant changes on Friday afternoon.

## Steps for Updating the Plugins

1. Send a message to the affected sites alerting our primary contact that we will be updating plugins on a specific day and time. The message should ask members to contact us via the [Largo Help Desk](https://support.largoproject.org) if they see any new issues after the update.
2. From the [WP Engine dashboard](https://my.wpengine.com/) for the appropriate install(s), create a backup point on production.
3. If conditions on staging allow, clone production to staging. 
4. Perform the plugin update(s) on staging.
5. Test the staging sites. See testing procedures below, which apply to both staging and production sites.
6. Perform the plugin update(s) on production.
7. Repeat the testing procedure on the production sites.
8. Make notes on any problems encountered and communicate to the relevant people.

## Testing

We’re going to begin with a visual inspection of the front-end of each site. Then we’ll look at the dashboard and verify the most important functionality. We want to look at the functioning of each plugin on a given site, and verify as much as possible that nothing is broken.

If you have our [wp-scripts tools](https://github.com/inn/wp-scripts) included in a given site's umbrella repository, you can see a complete list of activated plugins for each site by opening these urls in Chrome (must be logged in to see this):

`view-source:http://[installname].staging.wpengine.com/wp-scripts/list_active_plugins.php`

`view-source:http://[installname].wpengine.com/wp-scripts/list_active_plugins.php`

# Testing Steps

1. On production, clear the cache on WPEngine as it can sometimes prevent page elements from rendering properly after an update. Staging isn’t cached so don’t worry about it there.
2. Visit the front end of each site to verify that it’s rendering normally. On staging, compare the rendering of the following areas to their display on the not-yet-upgraded production server:
	- The homepage
	- At least one post
	- At least one page
	- Any pages generated or dependent upon plugins
3. Make note of any new issues. We’ve never had a total meltdown but if the front end is badly broken on production after clearing the WPEngine cache we’d want to restore from the backup point immediately.
4. Visit the dashboard of each site. We’re going to do a bunch of tests to make sure the site is functioning normally. 
	- Do a quick visual inspection of the dashboard home to verify everything is looking normal.
	- Open and verify the Posts list page.
	- Open a single Post in the post edit screen and verify the fields and panels are displaying everything normally.
	- Create a new Post and save it as a draft. Verify that it previews normally, then trash it. On staging you can publish the post and verify before trashing.
	- Open the Media Library and verify that images and any other media are displaying normally. Upload an image to verify it uploads, then you can delete the image.
	- Open Appearance > Theme Options and click thru the tabs to verify that everything appears correct.
	- Open Users and make sure things look normal.
5. Now look at the site’s plugins to verify they’re OK.
	- Check the list of plugins for a given site using the links above. Flag any plugins known to be problematic. These tend to be junky plugins we've installed for only a single site and they all know that we are not able to offer our usual support around updates for these plugins (i.e. - they need to pay for the work to update them if the updates don't go smoothly).
	- For any plugins that have their own settings, check these to verify they appear normal. This is especially important for plugins that require API keys or other connections to third-party services.
	- On staging at least you can further test the functioning of plugins, for example in test posts. Testing is going to depend on the plugins, but be as thorough as possible to verify everything is working correctly. 
6. If anything is awry make thorough notes, and take appropriate actions to remedy. In worst case we’ll need to restore from the backup point, but if so this must be done very soon to avoid loss of content published after the backup point.