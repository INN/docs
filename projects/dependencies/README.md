# Dependencies folder

This folder should contain a list of project dependencies, where the following are true:

1. the dependency is directly embedded in the project, as opposed to being served via a CDN, loaded with `npm` or `composer` or `pip`, or installed globally on the machine running the software. Embedded dependencies' code is tracked directly in the same repository as the project using it.
	- [Pym.js](blog.apps.npr.org/pym.js/) loaded via the CDN should not be here.
	- Pym.js files kept in the repository should be listed here.
	- Pym.js files uploaded somewhere for a project, but not actively tracked in that project's repo, should be listed here.
2. the dependency is not a software-as-a-service API that we expect to continue existing. This list includes non-beta products of the following companies: Amazon AWS, Google Drive.
