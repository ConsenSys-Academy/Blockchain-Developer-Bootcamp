# Contributing to Basic Training

## Why Contribute

Contributing to Blockchain Developer Bootcamp is a great way to [learn how to work on open source projects](https://opensource.guide/how-to-contribute).

This skill is essential because the overwhelming majority of blockchain-based projects are built via open source. If you can inspect the code, you can trust the code.

Contributing will help you improve:

- the software you use
- your existing skills
- your job prospects
- how you work with a team
- the chances to find mentors and network.
- your people skills

Although it may seem challenging, contributing to an open-source project gets easier after doing it the first time.

Stick with it, and you will master these small but essential skills.

Between participating in hackathons and contributing open source projects, they are the best way to land a job in the Ethereum ecosystem.

## Background

### Coordination

We use [github issues](https://github.com/ConsenSys-Academy/Blockchain-Developer-Bootcamp/issues) for our issue tracking and project management.

### Overview

We use the [Forking Workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/forking-workflow) method of open source contribution. This method allows projects to scale well with not alot of complexity.

### Setup

See the [primer on setting up repos](https://docs.github.com/en/get-started/quickstart/fork-a-repo).

1. [Fork](https://docs.github.com/en/github/getting-started-with-github/quickstart/fork-a-repo) the `ConsenSys-Academy/Blockchain-Developer-Bootcamp` [repository](https://github.com/ConsenSys-Academy/Blockchain-Developer-Bootcamp).

2. [Clone](https://docs.github.com/en/github/creating-cloning-and-archiving-repositories/cloning-a-repository-from-github/cloning-a-repository) the forked repository from your GitHub profile to your desktop.

3. [Add the remote](https://docs.github.com/en/github/collaborating-with-pull-requests/working-with-forks/configuring-a-remote-for-a-fork) repositories for [origin and upstream](https://stackoverflow.com/questions/9257533/what-is-the-difference-between-origin-and-upstream-on-github).  

Learn more about [working with forks](https://docs.github.com/en/github/collaborating-with-pull-requests/working-with-forks) 🍴.

## Contributing Code

### Issues

[Open a issue](https://github.com/ConsenSys-Academy/Blockchain-Developer-Bootcamp/issues).  Issues are good! They are used to point out errors and suggest new features.

### Picking up an Issue

Read the issue. Ask any questions in the issue thread. Mention the issue that you'd like to work on this to avoid double work.

### Staying Up To Date

Before starting on work on the issue, make sure your code is up to date.

1. Check your branch:  
 `git branch`
2. Checkout the main branch of your local repo:  
`git checkout main`
3. Fetch changes from the `upstream` main repo:  
`git fetch upstream main`
4. [Rebase](https://www.atlassian.com/git/tutorials/rewriting-history/git-rebase#:~:text=Rebasing%20is%20the%20process%20of,of%20a%20feature%20branching%20workflow.) the changes from the `upstream` master repository into your local repo:  
`git rebase upstream/main`
5. [Re-synchornize](https://www.togaware.com/linux/survivor/Git_Merge_Master_into.html) `main` into `dev` by merging:  

```
git checkout dev
git merge origin/main  
git push
```

Learn more on [how to use branches](https://www.atlassian.com/git/tutorials/using-branches) 🌳.

### Creating a contribution

1. Check for the latest code and update.
2. Branch off of `dev`.
3. Name your branch based on intent. See the style guide below.
4. Write code.
5. Commit code. See style guide.
6. Push the branch to `origin`.
7. Open a pull request with the branch.

## Style Guide

To keep our commit history clean, we follow these simple rules.

### Naming Git Branches

Types of branches:

1. `main` - main branch that is live.
2. `feat/FEATURE` - for features.
3. `fix/THING1` - hot fixes.
4. `bug/THING2` - bug fixes.

Make sure to:

1. branch your `feat/`, `fix/`, or `bug/` branches off `main`.

### Git Commit style guide

1. The First `-m`: High-level description  
`"Added| Edited | etc. FILE"`

2. Second `-m`: Describe the code in under 240 characters.  
`Added x feature in sample.js and updated README.md in the section required.`

```
git commit -m "Feature. Added GIF to README.md -m "Added the GIF was required to explain what is Solidity."
```

### Pull Request Commits

Make sure to [reference the issue that you are closing](https://docs.github.com/en/issues/tracking-your-work-with-issues/creating-issues/linking-a-pull-request-to-an-issue).

Example: `Closes #7 - Add CONTRIBUTING.md`

### Content style guide

Keep it brief but descriptive. Use links. Avoid jargon. 

When possible, use pictures or gifs.

## Get Support

Open an [issue](https://github.com/ConsenSys-Academy/Blockchain-Developer-Bootcamp/issues) or [join our discord](https://bit.ly/ConsenSysDiscord).

Made with ❤️ by ConsenSys and 
![GitHub Contributors Image](https://contrib.rocks/image?repo=ConsenSys-Academy/Blockchain-Developer-Bootcamp)