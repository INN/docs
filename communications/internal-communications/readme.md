# Internal Communications

## Overview

This document is intended for INN staff, board members, volunteers and contractors who may interact with the technology team at various times in the course of their work but may not be as familiar with all of our internal processes or interact with us everyday.

Much of this information is covered in [our team docs](http://github.com/inn/docs) which are great if you want a deeper dive into how we work and how to work with us most effectively.

## Getting Help

Everyone gets stuck from time to time and we're here to help. Given the volume of requests we receive, we have processes in place for managing support requests that vary slightly depending on the need.

**General questions** or requests for documentation - [open a new issue](https://github.com/INN/docs/issues) on the [INN docs github repo](https://github.com/INN/docs). HipChat is also great for general questions, choose the most appropriate room and ask away!

**Help with INN web properties** (INN.org, journo.biz, newstraining.org, etc.) - open an issue on the [INN Website JIRA project](http://jira.inn.org/browse/INNDEV/) (login required, email [nerds@inn.org](mailto:nerds@inn.org) if you need access)

**Help with Largo** - use the [Largo service desk](http://jira.inn.org/servicedesk/customer/portal/4) (additional help can be found in the [knowledgebase](http://confluence.inn.org/display/LKB/Largo+Knowledge+Base) and [documentation](http://largo.readthedocs.org/)) or email [support@largoproject.org](mailto:support@largoproject.org).

**Email for general inquiries**: [nerds@inn.org](mailto:nerds@inn.org). This goes to the entire team and someone will get back to you as soon as we are able. Please try to avoid emailing team members individually regarding support requests as these are assigned and handled from a shared queue.

## Tools

#### HipChat

[HipChat](https://www.hipchat.com/) is an "always on" group chat application that we use for conversation throughout the day as well as to keep conversations visible to all members of a team or project. 

Instead of having one-on-one conversations, posting in the relevant chat room makes these conversations visible, searchable and archivable so that everyone involved can easily see what is going on and/or quickly catch up if they're out of the office.

This also has the effect of avoiding the at times unfortunate feeling that someone has been "left out of the loop" in a particular conversation.

HipChat also allows you to add links to important documents, resources or webpages and to upload files which are then also archived and searchable. This is a great way to share links to things like documentation, screenshots, mockups, etc. that you may want to be able to easily refer back to later.

For these reasons, HipChat is typically the best place to start most conversations regarding support or to ask questions about a project.

When we kickoff a new project we will typically create a closed room specifically for that project and add the people who are involved. If you feel like you're missing a conversation you can always ping one of your coworkers to make sure you haven't been left out inadvertently.

There are also several standing rooms:

- **The main INN room** - open to all INN staff, general conversation not specific to any particular project, updates the entire staff needs to be aware of, etc.
- **The open INN tech room** - open to all INN staff, member organizations, partners, etc.
- **The closed INN tech room** - just the tech team, some general team business, but mostly project discussions, commit/deployment messages, etc. that are relevant only to our smaller team

HipChat also allows for one-to-one private messages and audio/video chats. Typically this is best for conversations that are either not of interest to a larger group and/or are sensitive in nature (personnel matters, etc.)

You can also mention someone in any room to send them a notification using the @ sign followed by the person's username (@username) or send a notification to all members of a room using @all.

**Getting Started**

- Request an account by emailing [nerds@inn.org](mailto:nerds@inn.org).
- [Download HipChat apps](https://www.hipchat.com/downloads) for Mac/PC or various mobile operating systems. You can also access HipChat through your browser but the apps tend to be easier to use.
- Sign in and ping one of your coworkers to make sure you've been added to the relevant group/project rooms.

#### JIRA

[JIRA](http://jira.inn.org) is a project management and bug tracking tool we use for many internal projects as well as for client projects where time tracking is required for billing.

It's also the home of our [help desk system for Largo](http://jira.inn.org/servicedesk/customer/portal/4) and the [list of known issues and roadmap](http://jira.inn.org/browse/INNDEV/) for INN's own web properties.

Mostly you'll need to be able to login, create issues on projects and then track the progress of those issues. If you want a tutorial on how to use some of the more advanced features and/or want to create new projects, just [send us an email](mailto:nerds@inn.org) and we'll be happy to give you a walkthrough.

**Getting Started**

- The login URL for JIRA is: [http://jira.inn.org](http://jira.inn.org). If you don't have an account, email [nerds@inn.org](nerds@inn.org) and we'll create one for you.
- Once you log in you will see a menu at the top of the screen that allows you to select from the projects that you have been added to. Once you select a project you'll be able to see issues related to that project and can click "create" in the top menu to add a new issue.
- For issues you create, you will also (by default) receive email notifications anytime the issue is updated. You can also reply to these emails to add new comments to the thread associated with that issue.

#### GitHub

GitHub is typically used for managing code but it can be used for keeping tabs on different versions of many types of documents. You can think of it sort of like track changes in something like Microsoft Word, but applied to any file type.

We use it for many of our open source projects, such as [Largo](http://github.com/inn/largo) where we not only make the source code available and manage contributions to the codebase but also as a place to [organize the roadmap](https://github.com/INN/largo/issues) for upcoming features and to allow users to [report bugs or issues](https://github.com/INN/Largo/issues/new) with the software we write.

You will more than likely encounter GitHub either through reporting issues with Largo or in reading, suggesting additions or contributing to [our team docs](http://github.com/inn/docs).

**Getting Started**

- Visit [http://github.com](http://github.com) and create an account.
- Email your username to [nerds@inn.org](mailto:nerds@inn.org) so we can add you to the INN team account and give you access to the relevant repositories.
- Click on the "issues tab" of any repository (for example, the INN docs repository: [https://github.com/INN/docs/issues](https://github.com/INN/docs/issues)) and then click on the green "new issue" button to create a new issue. You will automatically be subscribed to notifications when someone comments or updates the issue.

**Want to learn more about git?** Here are some resources and tutorials to help you get started:
	
- [How To Use GitHub and the Terminal: A Guide](https://18f.gsa.gov/2015/03/03/how-to-use-github-and-the-terminal-a-guide/) (18F)
- [How the Heck Do I Use GitHub](http://lifehacker.com/5983680/how-the-heck-do-i-use-github) (lifehacker)
- [Got 15 minutes and want to learn Git?](https://try.github.io) (Code School)
- [How to Git](https://github.com/tensory/HowToGit) (Ari Lacenski)
- [Getting Git Right](https://www.atlassian.com/git/) (Atlassian)
- [GitHub for Journalists](http://knightlab.northwestern.edu/2013/06/13/getting-github-why-journalists-should-know-and-use-the-social-coding-site/) (Knight Lab)

## Other Opportunities to Interact With Us

- **[Open Office Hours](/projects/office-hours/)** are held the first Thursday of the month from 4-6pm ET. These are primarily intended as an opportunity for members to sign up for a slot and come ask us questions, get feedback on work in progress or present a project that they've recently completed. These are held via Google Hangout and are completely open to anyone, including any INN staff that would like to attend.
- **[Book Club](/projects/book-club/)** is held the second Wednesday of each month at 1pm ET. This is a monthly book discussion, open to anyone, held via Google Hangout.
- **All of our regular team [meetings](/how-we-work/meetings.md)** are not strictly limited to our team and anyone from INN is welcome to attend. This includes our morning scrum (at 10am ET) and our weekly recap and planning meeting (Friday, 10:15 ET). These meetings are all conducted via Google Hangout. If you'd like to be added to the recurring event invitation for either (or both) of these meetings just [send us an email](mailto:nerds@inn.org) and we'll add you.


