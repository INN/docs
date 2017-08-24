# How to sunset a project

This document derives from the SRCCON 2017 talk [Let's Talk About Death 💀](https://etherpad.opennews.org/p/SRCCON2017-death-of-a-project).

The end-of-project planning process should begin early in the project lifetime.

There are four general categories of ending a project:

- **Handoff**: Someone else is taking over the project.
- **Archive**: We're no longer maintaining the project, but it's still useful in its current state.
- **Shutdown**: We're no longer maintaining the project, and as a result it is no longer useful.
- **Murder**: We're actively killing this project and ensuring that it cannot be used in the future.

In each case, prepare a document answering the questions for that section.

## Handoff

Someone else is taking over the project, so we need to ensure that they have all the resources necessary to continue it.

An example of this happening in another organization is Sunlight Foundation's Politwoops service and Congress API being adopted by ProPublica.

- Why was the project started? What are its goals?
- Who worked on this project, what did they do, are they open to being contacted about this project, and if so what should they be contacted about?
- What were major decisions made during the project? What were major events during its development?
- How does the project work? What are its features?
- What information is needed to maintain this project? Examples include accounts, credentials, domain name renewal dates, cost of hosting.
- Who is taking over, and why were they chosen?
- Why are we doing this handoff?
- Who uses this project?
- What else relies upon this project?
- What does the roadmap look like for the future of the project?

## Archive

We're no longer maintaining this project, but in its current state it may still be useful for other people.

## Shutdown

We're no longer maintaining this project, and as a result it is no longer useful. An example of this is when Sunlight Foundation shut down all its projects: because the databases required hosting and were not static, they would not be useful going forwards. Another example is Google Reader.

## Murder

This project needs to no longer exist. No one should use it. People who are using it should stop. 

- Why are we killing it?
- How should the project be terminated? Can we push an update that disables the software, or do we need to contact users and ask them to turn off the software?
- How do we contact users?
- What sort of public announcement of death needs to be made?
- Should we release the obituary before, concurrent with, or after the murder?
	- Before: when you don't have to shut it down immediately, but know that it must be shut down. "WordPress version 6.0 breaks this plugin by removing functionality that the plugin depends upon, and there is no way to build equivalent functionality in WordPress 6. As a result, this plugin will cease to be maintained, and will be removed from the WordPress.org listing, to avoid confusion."
	- Concurrent: software with an actively-exploited, unfixable, security hole should probably be murdered at the same time the obituary is released: "Effective immediately, we are shutting down Twitter, because its use has a 50% chance of people turning into waterfowl."
	- After: software that could be exploited, but is not currently being exploited. "The last release of this plugin removed the ability to make chickens blue, and the reason was not specified at the time the plugin was released. The reason for that release was because using the plugin to turn chickens blue (something 1% of users have ever done) could cause servers to accept invalid passwords at login, allowing anytone to access the site as an administrator. We elected not to make this announcement until such time as all users had upgraded to the latest version of this plugin."
