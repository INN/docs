# Anatomy of a Pull Request and Submission Protocol

A pull request (PR) is a request to merge changes you have made to an existing branch of a project. For specific guidelines on which branch to submit pull requests to, see the contributing guidelines in that specific project repo (usually in a contributing.md file at the root of the project).

Here are some guidelines for what information to include in your PR, when to submit a PR and when to wait to submit one. 

Remember that a PR is part of a process to document the changes to a product or procedure, so the more information you provide, the better you and your teammates will understand the purpose of your PR.


### What information to include in a PR

A PR should contain commits that are related and that address only one functional change. If you made changes to unrelated documents, projects, or various feature or issues, you should submit separate pull requests for each one.

To explain your PR, include:

- Explanation of the issues (including specific issue numbers) the PR addresses
- Explanation of **why** you chose to make these changes and any notes on your methodology or process that would be helpful to the person reviewing the request. We need to know not only **what** you changed but also the rationale behind your decisions.
- Any new issues or conflicts that your changes might create.
- Screenshots or useful links to explain your PR wherever relevant

Before submitting a PR, please also make sure you have removed any debugging code (var_logs, etc.), commented out code and unnecessary code comments (such as pseudocode or your personal notes).

### FAQs

##### When should I submit a PR?

Submit a PR when you have finished making changes to address one feature, issue, bugfix, piece of documentation (or closely related pieces) and believe your changes are ready for our team to review and merge back into the working branch of the project.

##### When should I *not* submit a PR?

Wait to submit a PR if you still have more edits to do or more content to add. Make more commits and combine them into a single PR if they are related to the same fix. **Do not be intimidated to submit PR!** When in doubt, ask our team for help. We may ask you to make changes and resubmit but this at least starts the conversation.

##### What should I expect after submitting a PR?

After your submit a PR, designated team members (usually a primary and secondary reviewer for each of our projects as designated in the project's contributing.md) will get a chance to review your work. Your PR may undergo changes before it is merged, so don't be surprised, discouraged, or hurt if we ask you to change things or if we make changes ourselves. 

##### What does a good PR look like?

Check out this [beautifully documented PR](https://github.com/INN/Largo/pull/646) by @benlk.  
 

### Inspiration

- [Texas Tribune Pull Request Template](https://gist.github.com/risatrix/ceabdf7e8d00f9dbdd38)
