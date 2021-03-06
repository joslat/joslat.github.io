---
layout: post
title: Contributing, A hands-on guideline for contributing to HotChocolate
subtitle: Let's give a hand to these smart gentlemen..
image: /img/chillicream-favicon.jpg
tags:
  - OSS
  - Backend
  - GraphQL
  - HotChocolate
published: true
date: '2020-04-27'
---


# What's this?
I decided to jump into getting the GIST of Open Source in a hands-on way, this blog post will be my second PR into the Hot Chocolate project, located [here](https://github.com/ChilliCream/hotchocolate) ;)  
And why not also publish it as a blog post, maybe I can motivate somebody else into jumping in and giving it a try! 
And, if so, please let me know :)


# Contributing!
When contributing to this repository, please first discuss the change you wish to make via Slack with the core team before making a change.
You can do so by joining the [slack group](https://join.slack.com/t/hotchocolategraphql/shared_invite/enQtNTA4NjA0ODYwOTQ0LTViMzA2MTM4OWYwYjIxYzViYmM0YmZhYjdiNzBjOTg2ZmU1YmMwNDZiYjUyZWZlMzNiMTk1OWUxNWZhMzQwY2Q). and suggest your idea in the #contributors channel.

Please note that there is a "Code of Conduct", which is located [here](https://github.com/ChilliCream/hotchocolate/blob/master/CODE_OF_CONDUCT.md). Be sure to follow it in all your interactions with the project, team and collaborators.

---
This guide will drive you through a successful execution on how to collaborate with this concrete project.

## Some prerequisites
This guide expects you to be some how familiar with GIT and the GitHub platform, as well as some .NET and C# Framework and language knowledge, as well as of the development tools, VS Code or Visual Studio. If you do not know the fundamental concepts and how to operate with it, well it's time to go back to basics and then come back.

One more thing, be sure to read the "Code of Conduct", which is located [here](https://github.com/ChilliCream/hotchocolate/blob/master/CODE_OF_CONDUCT.md)
It is quite generic, common sense, but also good to have a clear understanding.
In addition, you can also check the How-To-Contribute guide for Open source located [here](https://opensource.guide/how-to-contribute/)

## The Flow
The steps that we need to follow to collaborate are indeed simple:   
1. Pick or have an issue asigned or also, create it yourself (User & Team).  
2. Have some attributes added to the Issue such as Tags, Roadmap (Team).  
3. Either Fork the repository or create a branch for working on the issue (User).  
4. Write the code to implement or fix the Issue (User).  
5. Create a PR (Pull Request and link the PR to the Issue (User).  
6. Review and approve the PR (Team).  

Note: User is you, the valiant OSS Contributor. Team means the HotChocolate Team.
Note: If you are not a member, you will probably need to do a fork.

## 1. Pick an issue.
For this example, we are going to get an existing issue, concretely this one: [https://github.com/ChilliCream/hotchocolate/issues/1761](https://github.com/ChilliCream/hotchocolate/issues/1761)   
![01_Issue.PNG](https://github.com/joslat/joslat.github.io/blob/master/img/01_Issue.PNG?raw=true)


Note, this was taken after discussing a simple task I could take with one of the HotChocolate Core Team components, Pascal Senn. A really nice guy.

Otherwise, you can go to the list of open issues and pick the one you like and are confident you can take.  
The project is hosted at github.com, at [https://github.com/ChilliCream/hotchocolate](https://github.com/ChilliCream/hotchocolate)
And the list of issues is here: [https://github.com/ChilliCream/hotchocolate/issues](https://github.com/ChilliCream/hotchocolate/issues)  

Last but not least you should get that issue assigned to you so nobody else starts working on it, that should be done by a Team member. It also is a good idea to subscribe to the notifications on this issue.


## 2. Review or add the attributes to the Issue.
As we saw, the attributes seemed to be there, it has the labels Bug & Hot Chocolate.
The Roadmap is also assigned, this is assigned to [HC-11.0.0](https://github.com/ChilliCream/hotchocolate/milestone/45)
So, done - Next!

## 3. Fork the repo and create a branch for working on the issue.
Following, we will either create a branch directly if we have permissions or fork the repository and create a branch on our fork.

As at the moment of writing I do not have permissions I will follow the somehow longer path of creating a fork and then a branch on it.

### Forking the project's repository
Following the GitHub [guidance](https://guides.github.com/activities/forking/) we will go to the project main page and click on the Fork button.
![02_Fork.PNG](https://github.com/joslat/joslat.github.io/blob/master/img/02_Fork.PNG?raw=true)
And once it's done we should see a popup pointing to your forked repository.
![03_Forked.PNG](https://github.com/joslat/joslat.github.io/blob/master/img/03_Forked.PNG?raw=true)
Congratulations, you have successfully forked the HotChocolate repository!

To be able to work on your issue, we need to clone it to our computer.
In our github cloned project, we will go to the "Clone or download" green button and expand it, to copy the git URL clicking the button at the right side of the URL.
![04_clone.PNG](https://github.com/joslat/joslat.github.io/blob/master/img/04_clone.PNG?raw=true)

We will open a command line and clone the repository in our local computer using command line GIT (or your tool of choice).
```bash
git clone https://github.com/joslat/hotchocolate.git
```

And that's it, we should have the repository on our computer.

### Create a branch for the issue
In GitHub, we will go to the Branch selector and type something meaningful that represents the work we are going to do.
For the issue, I picked "FIX-variable-stitching-v11" which details the work (fixing an issue) and some details on it as well as to what version it is tailored.

We will add the new branch name on the "find or create a branch" textbox and click on "create branch" button inmediately below.
![05_Create_Branch.PNG](https://github.com/joslat/joslat.github.io/blob/master/img/05_Create_Branch.PNG?raw=true)

Now we need to reflect this on our computer so we will go to our lovely command line interface and pull the remote branch:  
```bash
git pull
```
We should get as a result the following:  
```bash
From https://github.com/joslat/hotchocolate
 * [new branch]        FIX-variable-stitching-v11 -> origin/FIX-variable-stitching-v11
Already up to date.
```

That's it, our new branch is local and we are ready to start fixing the issue!


## 4. Write the code to Fix or implement the Issue.
Following, we will open the hotchocolate project with our favorite IDE, in my case Visual Studio.
We will first perform some actions in our computer to be sure we are ready to start working:
 - Get the right  branch.
 - Build the solution and make sure everything builds.
 - Run the tests and see where we stand at.
 - Implement the fix for the Issue.


### Getting the right branch
we will open the HotChocolate.sln solution, located in ./src/HotChocolate/  
And we will checkout the branch we want to work with:   
```bash
git checkout -b FIX-variable-stitching-v11 origin/FIX-variable-stitching-v11
or
git checkout FIX-variable-stitching-v11
```

And in the lower right corner of Visual Studio we should see that it reflects the current branch we are working in.   
![06_VisualStudio_WorkingBranch.PNG](https://github.com/joslat/joslat.github.io/blob/master/img/06_VisualStudio_WorkingBranch.PNG?raw=true)

### Building the solution
Here we will open the solution that we have to work on. If we peek again at the Issue, on the description it says "port #1746 to 11".  
We can click on the Issue 1746 to read it and learn what was done.
Mainly this is a port of some modifications in the Stitching solution plus tests performed on another branch corresponding to version 10. As this cannot be ported directly as there are structural changes, needs to be done manually using our favourite technique: "Copy-Pasta" ;).

The solution we opened is correct as it contains the Stitching folder where most of the files to modify are.

We will right click on the Solution and click on "Restore NuGet Packages". After this, we can proceed to rebuild the solution.


### Running the tests
We can do the usual; Test --> Run all tests.  
Note that some of them will fail, also some require docker and if you have it disabled as I do right now, will also fail.  

Once the tests are done, which might take a bit, we can see that the ones that matter for this issue, related to Stitching, are all "green":  
![07_StitchingTestsPass.PNG](https://github.com/joslat/joslat.github.io/blob/master/img/07_StitchingTestsPass.PNG?raw=true)


### Implementing the fix for the Issue
We have 23 files changed in the parent issue 1746, so we will proceed to open the files changed section of that issue and start applying the changes into our branch... 

Once this is done, tests run, we will:
- Commit the changes locally.
- Push them to the remote repository (our fork).


## 5. Perform a Pull Request PR to the original repository.
We are ready to create a PR, we will go to our Forked repository in github, select the branch and click on Create a Pull Request.  
We will fill it up with the detail of what has been performed.  
![08_createPR.PNG](https://github.com/joslat/joslat.github.io/blob/master/img/08_createPR.PNG?raw=true)

Once this is in we should add the same tags and attributes as the Issue, and link the issue manually to this PR.


## 6. Review and approve the PR.
This should be done by the team but the process can be observed in the Pull Request (we should get a link to it once we create the PR).

In our case, it is [here](http://github.com/ChilliCream/hotchocolate/pull/1801)
Nothing was as smooth as expected, there were some issues, some tests that did not pass due to differences from the branches where the fixes were taken, some tests mostly.

If any issue was caused that was overseen by running the tests locally then it would be our task to fix these issues and update the PR.

Aside from this once the PR is approved, it will be Merged into the main branch (or where the Issue or feature resides).  
The Issue will be closed too.  
And a Prerelease will be performed as well.
