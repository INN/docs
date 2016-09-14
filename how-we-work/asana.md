# Project Management with Asana 

The INN Product and Technology team is using Asana for our project management tool. It can be great for defining a project and dividing it into tasks, assigning team members, setting due dates, and tracking project assets etc. It can also generate a lot of noise. Here's how to achieve the former and avoid the latter.

## Scope of this document

We're assuming familiarity with Asana before reading this guide to how we use it at INN. (Provide some links to resources here)

## New Projects

In the Projects list in Asana, there's a project named **Template: New Project**. This should be used to create any new projects. To do that, hover over the three dots to the right of the project name, click to open the Project Actions menu, and select **Copy Project (Use as a template)**:

![Creating a new project in Asana by compying the New Project Template](.img/asana-new-project-menu.png)

This will open the New Project dialogue box where you give it a project name. You can leave the checkboxes as they are and click **Create New Project**. 

![New Project dialogue box](.img/asana-new-project-dialogue.png)

The new project appears in Asana's project list, yay!

### Project Description

After creating a project, give it a short description so it's clear to all concerned what it is. Click on the project name in the Asana project list, then click the dropdown arrow on the right side of its name:

![Editing a project in Asana](.img/asana-edit-project.png)

Add the project description, which in most cases should be a single sentence. You can also add this project to your Asana dashboard, give it a different highlight color, etc.

## Project Structure

The default project layout provides a structure for defining tasks:

- New To-Do Items: New tasks that have come in (perhaps from a client) but have not yet been reviewed/scheduled.
- Now: Tasks that are part of the current sprint (due before the next iteration review, typically in a week or two)
- Next: Tasks that will be included in the next sprint. To be reviewed/assigned/scheduled at the next iteration review.
- Upcoming: Tasks that will be included in a future sprint (stuff we know we need to do but have not yet scheduled).
- Backlog: Nice to have items that we may or may not get to depending on the time/budget available for any given project.
- Questions: Questions we have for stakeholders/clients that need to be resolved before defining tasks and scheduling future work
- Project Management: Meetings, communication, etc, e.g. setting up a project Slack channel

You should use this structure to begin creating tasks. 

Tasks define the specific work to be done. If written correctly, completion of the project tasks completes the project. 

## About Tasks and Subtasks

Each task should require a maximum of eight hours of work. If you think a task will require more than eight hours of work, create subtasks within that task. (Subtasks can also have sub-subtasks but let's not get crazy.) Add descriptions to tasks and subtasks as needed, but generally the subtasks should be written specifically enough to explain themselves.

Note that attachments can be added to tasks and subtasks for project resources, documentation, etc.

### Assigning Tasks and Due Dates

Tasks and subtasks should always be assigned to the team member responsible for their completion. You can also add Followers to tasks, who will then be notified when anything is done within that task. 

Due dates should be assigned to each task but **not to any subtasks** because this can get extremely noisey. 

### Adding Tags to Tasks and Subtasks

Asana provides for adding tags tasks, which makes it easier to identify at a glance things like priority, how long the task is expected to take, if it needs docs or subtasks, etc. 

We use a standard set of tags which are defined in this [sample Asana ticket](https://app.asana.com/0/116212059113593/116212059113594).

Clicking a tag in any task opens other tasks that have that tag. So it's easy to see all tasks that are tagged "Priority" etc.

Definitely assign tags to tasks and subtasks as you create them, and add them as appropriate.

## Time Tracking

Asana has an integration with Harvest that lets you track time right from the Task view in Asana.

![Asana Time Tracking Feature](asana-time-tracking.png)

Best practice is to start Asana's time tracking when you start work on a task, then stop the clock in Asana when you stop working on that task. 

### Asana/Harvest Time Tracking Gotcha

Due to synch peculiarities, when you stop the clock on a task in Asana then switch over to Harvest, time tracking for that task may look like it's still running. If you refresh the browser tab where you have Harvest, the clock will show that it's been stopped. But if you already stopped the clock in Asana, then stop the clock in Harvest, the Harvest clock for that task will return to 0:00. This leads to incorrect time tracking for the task, and potential billing errors on client projects which we don't want.
