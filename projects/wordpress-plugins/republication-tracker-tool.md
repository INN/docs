# Republication Tracker Tool

Status: Maintained?

## Relevant links:

- GitHub repo: https://github.com/INN/republication-tracker-tool
- Wordpress.org plugin repo: https://wordpress.org/plugins/republication-tracker-tool/
- Documentation: https://github.com/INN/republication-tracker-tool/blob/master/docs/README.md
- Documentation: https://support.inn.org/category/313-republication-tracker-tool-plugin


## What is it?

Republication Tracker Tool began life as the "Creative Commons Sharing" plugin, which provided a means to facilitate sharing the content of a post under a Creative Commons license. RTT extends that with a tracking mechanism similar to ProPublica's [PixelPing](https://www.propublica.org/pixelping). RTT's tracker is presented to the reader as the logo of the site of original publication, but on the server side is a redirect to an image file, which logs information about the referrer to Google Analytics and the publishing site's database as post meta.

Provides:
- a sharing button that opens a modal
- a modal that provides information about this site's sharing policy
- a way to copy the text of a story to facilitate pasting it into other sites' CMSes
- a tracking bug in the form of an `img` tag
- an image URL that redirects through a hit counter, which tracks hits and referers within WordPress and by sending hits to Google Analytics to track republished articles from external websites.


## Who made it?

RC Lations did a lot of the initial work, with support from Julia Smith. Since then, it's been mostly Ben Keith and Josh Darby, with some outside support from INN members.

## Things to know

This plugin powers republication buttons on sites that don't use the plugin's own code for outputting the share modal. Be cautious about deprecating existing code.

Known examples:

- https://19thnews.org/2020/08/black-women-economy-coronavirus-systemic-racism/?republish
- https://ohiocapitaljournal.com/briefs/operation-grant-seeks-to-turn-republicans-toward-biden-in-election/
