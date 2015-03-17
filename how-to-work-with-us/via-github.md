# Contributing to the INN Nerds docs repo using Github.com

This guide is for those of us who are not regular Terminal/shell users and those who do not want to or can't use the Gitbub client to make changes to a Github repository.

While this is written specifically for folks that want to contribute to our docs repo, the steps are the same for any repo.

Keep in mind that our docs repo is just a collection of Markdown files, making it an ideal candidate for this approach to contributing.

Since you can't run your code on Github.com to test changes, the potential to introduce bugs by editing code directly on Github.com seems extraordinarily high, in my opinion. If you have a repo with actual code, I'd suggest learning command line git or dive into the Github client. The learning curve is steep, but the tools are more powerful.

## Getting started

First of all, you'll need a [Github.com account](https://github.com/join) if you don't already have one. It only takes a minute. We'll wait for you.

After you have your account set up, go to the [INN docs repository](https://github.com/INN/docs).

From there, you can use the "Fork" button in the top right to create a full copy of the repository under your Github account.

![Fork this repo](http://assets.apps.inn.org/github-tutorial/fork-this-repo.png)

If you are a member of multiple organizations on Github, you will be asked where you'd like to fork the repository. In this case, I want my fork of the docs repository to live under my personal Github account:

![Choose account for fork](http://assets.apps.inn.org/github-tutorial/choose-account-for-fork.png)

After you choose an account, Github creates your new fork and drops you on its homepage. Notice the URL and the message just below the title of the fork indicate that this is a derivative of another repository.

![Fork homepage](http://assets.apps.inn.org/github-tutorial/after-fork.png)

Step one: complete. Not so bad, right?

## Editing a file

Now let's make a simple change to one of the files in our fork of the repository. In this case, we're making a superficial change to the README.md file as an example.

From the homepage of the fork, find the README.md link and click:

![README.md](http://assets.apps.inn.org/github-tutorial/readme.png)

Once the README.md has loaded, look for the edit icon near the top on the right side of the page:

![Edit README.md](http://assets.apps.inn.org/github-tutorial/edit-readme.png)

Once you click the edit icon, you are presented with a text editor where you can make changes to README.md:

![Editing README.md](http://assets.apps.inn.org/github-tutorial/editing-readme.png)

Towards the bottom of the file, I notice that the spacing between the heading `Version 0.1` and the list that follows is not consistent with the style of the rest of the document. So, I add a new line after `Version 0.1`.

Before and after:

![Before and after](http://assets.apps.inn.org/github-tutorial/before-and-after.png)

Next, we must add a message to along with our change. At the bottom of the page, you'll see an area labeled "Commit changes". In the first input, you should provide a brief but sufficiently descriptive message regarding your change, so that anyone browsing the history of changes made to the repository will have an idea of what changed and when. For example:

![Commit message complete](http://assets.apps.inn.org/github-tutorial/commit-message-complete.png)

The secondary input is optional. I'm going to skip it here.

Once your message is in place, click "Commit changes".

## Submitting a pull request

Great! Now you have your own fork of the repository and you're making changes left and right. But how do we let the maintainers of the original repository know that we have lots of good stuff for them to incorporate in the original?

The answer: submit a pull request.

To do so, go to the homepage of your fork. In my case, https://github.com/rnagle/docs. Towards the top, right side of the page find the "Pull request" link and click.

![Pull request](http://assets.apps.inn.org/github-tutorial/pull-request.png)

On the page that follows, you'll see something like:

![Pull request details](http://assets.apps.inn.org/github-tutorial/pull-request-details.png)

If you've followed these instructions, the pull request page should default to settings which essentially say "Submit a request to the maintainers of the original repository, asking them to pull in the changes made to my fork of this repository."

We'll gloss over the details of what each of the dropdowns at the top of the page can do for the pull request settings. Let's stick with Github's sensible defaults for now.

Towards the bottom of the page, you can see the "diff" (i.e., difference) between the original version of the README.md file (left) and the changes made to the README.md file in your fork.

Now, click the big green "Create pull request" button at the top.

You'll be presented with another dialog, asking you to include any relevant details about your changes, consequences it might have for other areas of the repository, why your change is the "right way" to do it, etc.

![Pull request details](http://assets.apps.inn.org/github-tutorial/pull-request-message.png)

Once you add a sufficient message, click "Create pull request" (this time, with feeling!).

Hooray! We now have an open pull request on the original repository's page:

![Open pull request](http://assets.apps.inn.org/github-tutorial/open-pull-request.png)

Note that the URL and the repository title no longer reflect our Github account or fork of the repository.

## What happens next?

When you submit a pull request, a notification is sent to the maintainer(s) of the repository. They can then review your proposed changes and either merge (e.g., pull) your changes back into the original repo.

In this case, since I am a maintainer for the original repository, the pull request page in the screenshot above displays a "Merge pull request" button. This will not appear if you do not have permission to make changes directly to the original repository.
