---
title: Managing your Teams/Components
layout: article
section: Developing Components
category: component
order: 1
---

When developing your own [integration components](/getting-started/integration-component) for the {{site.data.tenant.name}} platform, you need to structure your work into Git
repositories. Each repository represents an integration component and gets used
to push your local code to {{site.data.tenant.name}} remote server. Every push
results in a new deployment of the component.

The access to the component repository is restricted to a team the repository
belongs to. Each member of the team can change, configure and deploy a component.
The team itself belongs to the contract and so only members of the contract can
be invited to the team.

## Manage developer teams

A developer team controls access to the component repositories belonging to that
team. The team members may collaborate on common integration component in integration projects.

### Creating a developer team

> **Note**: you must have contract `Admin` privileges for this to work.

To create a new developer team navigate to the **Settings** section as shown
on the screenshot below:

![Settings section](/assets/img/developer-guide/team-repo/developer-team-01.png "Settings section")

You are now on you profile page. Here click on the name of your contract as shown:

![Go to the contract settings](/assets/img/developer-guide/team-repo/developer-team-02.png "Go to the contract settings")

On the contract settings page click on the **Developer teams** tab as shown on
the  screenshot below:

![Navigate to the developer teams](/assets/img/developer-guide/team-repo/developer-team-03.png "Navigate to the developer teams")

Here you will find all the developer teams you are member of. If you see no teams
here then click on a button *+ Add New Team* as it shown on the screenshot below:

![Creating a team](/assets/img/developer-guide/team-repo/developer-team-04.png "Creating a team")

After clicking the button a menu is presented to enter the name of your team:

![Naming the team](/assets/img/developer-guide/team-repo/developer-team-05.png "Naming the team")

The naming of the team must adhere to specific rules:

> **Note**: use letters, digits, `-` and `_` to name your team. No spaces!

After creating the team you are automatically becoming the member of that team.

![Explore the team](/assets/img/developer-guide/team-repo/developer-team-06.png "Explore the team")

You can proceed to either creating your first repository in this team and push your
custom component or you can invite your fellow developers into the same team to
collaborate in the development of that particular component.

![Start inviting Developers](/assets/img/developer-guide/team-repo/developer-team-07.png "Start inviting Developers")

### Invite developers into your team

To invite your colleagues into your development team to work on the same custom
component click *Invite developer* button to be presented with the menu like this:

![Choose the Developers](/assets/img/developer-guide/team-repo/developer-team-08.png "Choose the Developers")

To invite a developer, click on the check-mark in front of the their names and then
click on the *Send Invites*. The developers will receive invitation by e-mail
and would need to accept it to join the team.

> **Note,** only members of the same contract can be invited into this developer team.
> The list shows all the possible members that can be invited to this current team.

You can skip to the integration component [repository creation section](#manage-integration-components)
from here. Otherwise if you need to delete a developer team continue to the next section.

### Delete the developers team

If you need to delete a developer team:
*   You should have contract admin access role and
*   The developer team must contain no integration component.

If the above conditions are true, you can proceed and delete the developer team using [an API call]({{site.data.tenant.apiBaseUri}}/v2/docs/#delete-a-team).


## Manage integration components

Almost every developer has worked with some sort of version control and repository
management. GitHub, one of the most famous code developing and collaborating platforms,
is the most famous for its use of repository practice. We use the same tactics which
give developers complete autonomy to manage their code.

> **Note**: Remind your fellow developers to follow the same procedure and upload
> their own unique SSH Key before proceeding further.

### Create a component repository

As mentioned above, each repository represents a component. That's why we use
repository and component terms interchangeably here. Every component resides in
a particular repository.

To create a repository click on *New Repo* button and input the desired name and press *Save*:

![Create Repository](/assets/img/developer-guide/team-repo/developer-team-09.png "Create Repository")

Fill-in the presented form to create the developer team.

> **Note: As with the naming of the teams use letters, digits, `-` and `_` to name your repository. No spaces!**

![Repository instructions](/assets/img/developer-guide/team-repo/developer-team-10.png "Repository instructions")

In this particular example, the name of the repository is `petstore-nodejs` and it
belongs to the `acme_dev`. The screenshot above includes further instructions and
guidelines on how to proceed further. Here are the necessary steps for the clarity:

1.  Upload SSH key - Please [upload your public SSH key](ssh-keys) here if you haven't uploaded it yet.
2.  Clone our "Petstore" component
```sh
git clone {{site.data.tenant.petStoreSourceNodeJS}}.git petstore-nodejs
cd petstore_nodejs
```
3.  Edit code to make your own component. Please read our documentation to learn how to implement your components.
4.  Push your code
```sh
git remote add component acme_dev@git.acme.co:petstore-nodejs.git
git push component master
```

### Manage the component repository

Here is how the main Development page would look like after the deployment of your custom component:

![The deployed component](/assets/img/developer-guide/team-repo/developer-team-12.png "The deployed component")

To manage your repository click on the name to see the following page with details:

![Component repository setup](/assets/img/developer-guide/team-repo/developer-team-11.png "Component repository setup")

#### Repository URL:

This is the URL that you can push the code for deploying the updates.

> **Note: the cloning of your repositories is not supported.** To update the code
> push it again to create the next version of it. Please contact our support if
> you need the copy of your repository.

#### Environment variables:

You can set all environment variables for this particular repository by following the link. Consult our documentation on How to define environment variables for integration components.

#### Access:

This feature gives a possibility to set the component as Private, Public and Global:

*   `Team` means accessible to the contract (this is the default).
*   `Public` means accessible for the entire tenant.
*   `Global` means accessible for all tenants - **can be set only by support**.

> **Note:** Only developers in this team can deploy updates, manage thes environment variables or delete the repository.

#### Build history:

Here is the deployment history of the repository containing:

*   The date of deployment
*   the version of the repository deployment and the commit ID.
*   Status of the build - check mark means success. If the deployment failed it will show a cross.
*   State of the build - showing which build is the default.
*   Log of the deployment - clicking the "View" button will open the deployment log.
