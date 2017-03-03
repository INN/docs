# INN News Apps And Technology Team Docs

### Table of Contents

**What's in here (so far):**

-  **[A manifesto](manifesto.md)** outlining our team's mission and values
-  **[Our Strategy for 2015](/strategy/2015.md)**
-  **[Staffing and Hiring](/staffing)** including how we recruit and hire new team members, plus:
    - [Some information](/staffing/hiring/application-process.md) on our application/interview process
	- [Sample job descriptions](/staffing/job-postings/readme.md) from our team and from INN member organizations
	- [Interview questions](/staffing/hiring/interview-questions.md) for screening candidates
	- [Our onboarding process](/staffing/onboarding)
-  **[How we work](/how-we-work)** including:
	- [Our internal process](/how-we-work/process.md) we follow for most of our projects
	- [What we've learned about working as a remote team](/how-we-work/remote-work.md)
	- [The tools we use](/how-we-work/tools.md)
	- [Notes on how we conduct meetings](/how-we-work/meetings.md)
	- [How we give feedback to other team members](/how-we-work/feedback.md)
	- [How we use GitHub and Git for version control](/how-we-work/version-control.md)
-  **[How to work with us](/how-to-work-with-us)** including:
	- [General guidelines](/how-to-work-with-us) for how to work with us effectively
	- [Services we offer to INN members](/how-to-work-with-us/member-services.md)
	- [Details of our paid consulting program](/how-to-work-with-us/consulting/readme.md)
	- [Intake documents](/how-to-work-with-us/intake-procedure.md) for new projects
	- [A code of conduct](/how-to-work-with-us/contributing.md) for contributing to our open source projects
	- [How to contribute to our projects using GitHub](/how-to-work-with-us/via-github.md)
	- [Guidelines for submitting great pull requests](/how-to-work-with-us/pull-requests.md)
-  **[Style guides](/style-guides)** for:
	- [Code](/style-guides/code)
	- [Design/ui](/style-guides/design) elements
	- [Data projects](/style-guides/data)
-  **[Projects](/projects)** we work on with descriptions of each project and relevant resources.
-  **[Checklists](/checklists)** to help keep us organized.
-  **[Our Communications Strategy](/communications)** including:
	-  External communications
		- [Our weekly newsletter](/communications/newsletter)
		- [Twitter accounts](/communications/twitter.md)
	- [Internal communications](/communications/internal-communications).

**What is not (and will not) be in here:**

-  Documentation for [Largo](http://largoproject.org) and some of our other large projects which will typically be kept with their respective project repos as well as on [Read the Docs](https://readthedocs.org/).
-  Documentation for our other apps/tools/etc. (e.g. our [deployment tools](https://github.com/INN/deploy-tools) or our [responsive tables](https://github.com/INN/responsive-tables) rig) that are on the smaller side will typically reside within those repos directly as a readme file at the root of the repository.

**Important Note:** Nothing in these docs supercedes what you'll find in the [INN employee manual](https://docs.google.com/document/d/1MkXPsg6nD3yAfwXWczhscdoze7QhHgsrd_vLK1uQPB4/edit). Always refer to that for any personnel, hiring, payroll, etc. issues.

### Thanks!

These docs draw on (and sometimes straight up steal) excellent work from teams that have come before us. Here are a few of our sources of inspiration:

- [ProPublica's News App and Data Style Guides](https://github.com/propublica/guides)
- The NPR Visuals Team's [app template](https://github.com/nprapps/app-template), [coding best practices](https://github.com/nprapps/bestpractices) and [manifesto](http://blog.apps.npr.org/2014/06/04/how-we-work.html)
- [Guides](https://github.com/newsapps/guides) and [Process Docs](http://blog.apps.chicagotribune.com/2014/03/05/everything-you-ever-wanted-to-know-about-the-news-apps-process/) from The Chicago Tribune's News Apps Team
- [MinnPost's UI Style Guide](https://github.com/MinnPost/minnpost-styles)

[![BrowserStack](data:image/png;base64,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)](https://browserstack.com)

The INN Nerds use <a href="https://browserstack.com" target="_blank">BrowserStack</a> to test our apps for cross-browser compatibility on real browsers. 

### License

All of these documents are licensed under a [Creative Commons BY-NC 3.0](http://creativecommons.org/licenses/by-nc/3.0/) license. You are free to share and to remix them (as long as you credit us) but please don't use them commercially without permission.

### Contributing

We welcome contributions and suggestions to help us improve any of these documents. Please start by [reading our contribution guidelines](/how-to-work-with-us/contributing.md) and then [review the specifics](contributing.md) for this project to get started.

### Who Wrote This?

The INN news apps and technology team is:

-  **[Gabriel Hongsdusit](https://github.com/gabehong)** ([@ghongsdusit](https://twitter.com/ghongsdusit)), Design Apprentice
-  **[Ben Keith](https://github.com/benlk)** ([@benlkeith](http://twitter.com/benlkeith)), News Apps Developer
-  **[RC Lations](https://github.com/rclations)** ([@rclations](https://twitter.com/rclations)), Lead Developer
-  **[Kay Lima](https://github.com/kaylima)** ([@kayleen_lima](http://twitter.com/kayleen_lima)), Support and Community Lead
-  **[Julia Smith](https://github.com/julia67)** ([@julia67](https://twitter.com/julia67)), Acting Director, Product & Technology

**Head Nerd emeritus:** **[Adam Schweigert](https://github.com/aschweigert)** ([@aschweig](http://twitter.com/aschweig))

**Nerds emeriti:** [Nick Bennett](https://github.com/tothebeat), [Jack Brighton](http://github.com/jackbrighton), [Will Haynes](https://github.com/willhaynes), [Kaeti Hinck](https://github.com/kaeti), [Dani Litovsky Alcalá](https://github.com/danilito19), [Denise Malan](https://github.com/dnmalan), [Meredith Melragon](https://github.com/meredithinn), [Ryan Nagle](https://github.com/rnagle), [Sinduja Rangarajan](https://github.com/cynduja) and [David Ryan](https://github.com/dryanmedia)

**Additional contributions from:** [@chriszs](https://github.com/chriszs) and [@brentajones](https://github.com/brentajones)

### Changelog

**Version 0.1**

- Initial Release

