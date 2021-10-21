# Technical Requirements

This course assumes a baseline of technical knowledge. It is important to make sure you are comfortable with the following tech. If you are not, we are providing links to excellent resources you can use to get up to speed! Please note that you can learn all these things in our free [Basic Training course.](https://courses.consensys.net/courses/bootcamp-basic-training){target=_blank}

*   [Unix / Linux Environment](#unix-or-linux-environments)
*   [Command Line](#command-line)
*   [Git](#git)
*   [JavaScript](#javascript)
*   [Code Editor](#code-editor)

## Unix or Linux Environments

To be successful in this course you must have access to a Unix or Linux based operating system. MacOS is based on Unix and if you're running Ubuntu, that's a Linux distribution.

**If you are on a Windows 10 machine, [follow this guide to installing a Linux environment](https://consensys.net/blog/developers/ethereum-developers-guide-to-setting-up-windows-subsystem-for-linux/){target=_blank} before starting the course.**

If you'd like to get more familiar with a Linux environment, you can check out this Ubuntu for beginners, targeting Ethereum Developers specifically:

*   [Ubuntu for Beginners](https://agstakingco.gitbook.io/ethereum-2-0-ubuntu-for-beginners/#linux-terminal-basic-commands){target=_blank}

(Those interested in learning more about the history of Unix can read [this excerpt](https://www.netmeister.org/book/02-unix.pdf) from _Advanced Programming in Unix Environment_ by Stevens and Rago)

## Command Line

The command line is the basic non-graphic interface for your computer. It is most commonly called the **terminal** or the **shell**.

To be successful in this course, you should be comfortable using the command line. Among other things, you should be very comfortable changing directories using `cd`, deleting files with `rm`, installing files with `curl`, and running programs from the command line.

We would also recommend becoming familiar with command line shortcuts, such as:

*   **CTRL + C** Interrupts and quits the process currently running. Crucial in stopping terminal line programs
*   **CTRL + A** Moves your cursor to the beginning of the line
*   **CTRL + E** Moves your cursor to the end of the line

Sometimes it's helpful to remap your caps lock key to become CTRL. Find out how to do that [here.](https://www.howtogeek.com/194705/how-to-disable-or-reassign-the-caps-lock-key-on-any-operating-system/){target=_blank}

To brush up on command line skills, check out:

*   [MIT: Your Missing CS Semester: The Shell](https://missing.csail.mit.edu/2020/course-shell/){target=_blank} and [Shell Tools](https://missing.csail.mit.edu/2020/shell-tools/){target=_blank}
*   [The Odin Project: Command Line Basics](https://www.theodinproject.com/courses/foundations/lessons/command-line-basics-web-development-101){target=_blank}
*   [Ubuntu for Beginners](https://agstakingco.gitbook.io/ethereum-2-0-ubuntu-for-beginners/#linux-terminal-basic-commands){target=_blank}

## Git

[Git](https://en.wikipedia.org/wiki/Git){target=_blank} is a [version-control system (VCS)](https://en.wikipedia.org/wiki/Version_control){target=_blank} used to track changes made to projects. While git seems simple, it's actually a bit challenging to get comfortable with. (Note that git is a piece of software, on which version control sites like GitHub or GitLab are based.)

Here are some resources to get you started:

* [Git: Docs](https://git-scm.com/doc){target=_blank}
*   [The Odin Project: Setting Up Git](https://www.theodinproject.com/courses/foundations/lessons/setting-up-git){target=_blank}
*   [The Odin Project: Git Basics](https://www.theodinproject.com/courses/foundations/#git-basics){target=_blank}
*   [MIT Missing CS Semester: Version Control (git)](https://missing.csail.mit.edu/2020/version-control/){target=_blank}
*   [Git and GitHub for Poets (video)](https://www.youtube.com/playlist?list=PLRqwX-V7Uu6ZF9C0YMKuns9sLDzK6zoiV){target=_blank}


Not only is git a part of a good coding repertoire, it's also used by many [open-source projects.](https://www.digitalocean.com/community/tutorial_series/an-introduction-to-open-source){target=_blank} An essential part of the bootcamp is contributing to open-source projects. It's really important to know how to do proper Pull Requests and other guidelines for contributing to open-source. Here are a few resources to help you with this:

*   [GitHub Pull Request Tutorial](https://guides.github.com/activities/hello-world/){target=_blank}
*   [On undoing, fixing, or removing commits in git](https://sethrobertson.github.io/GitFixUm/fixup.html){target=_blank}
*   [How to Teach Git](https://rachelcarmena.github.io/2018/12/12/how-to-teach-git.html){target=_blank}

For those who would like to get a headstart, check out the "Good First Issues" for these open-source Ethereum projects:

*   [MetaMask](https://github.com/MetaMask/metamask-extension/issues?q=is%3Aissue+is%3Aopen+label%3Aux-enhancement+-label%3AN00-needsDesign+label%3Agood-first-issue){target=_blank}
*   [Truffle](https://github.com/trufflesuite/truffle/issues?q=is%3Aopen+is%3Aissue+label%3A%22good+first+issue%22){target=_blank}
*   [Go Ethereum (geth)](https://github.com/ethereum/go-ethereum/issues?q=is%3Aopen+is%3Aissue+label%3A%22good+first+issue%22){target=_blank}
*   [Web3.js](https://github.com/ChainSafe/web3.js/issues?q=is%3Aopen+is%3Aissue+label%3A%22Good+First+Issue%22){target=_blank}
*   [Prysmatic Labs](https://github.com/prysmaticlabs/prysm/issues?q=is%3Aopen+is%3Aissue+label%3A%22Good+First+Issue%22){target=_blank} or [Teku](https://github.com/ConsenSys/teku/issues?q=is%3Aopen+is%3Aissue+label%3A%22good+first+issue+%3Araising_hand%3A%22){target=_blank} (Ethereum 2.0 client)

Be sure to read Community Guidelines before contributing to a project. For example, here is Geth's [Contributor Guidelines](https://github.com/ethereum/go-ethereum/wiki/Developers'-Guide#contributing){target=_blank} and their [Code Review Guidelines](https://github.com/ethereum/go-ethereum/wiki/Code-Review-Guidelines){target=_blank}

## JavaScript

Even if JavaScript is not your first software language, it's really important you be familiar with its basic syntax. [Solidity,](https://docs.soliditylang.org/en/v0.8.2/){target=_blank} the smart contract language you'll learn, is based on [ECMAScript.](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Language_Resources){target=_blank} We recommend [Code Academy's free Intro to JavaScript course,](https://www.codecademy.com/learn/introduction-to-javascript){target=_blank} [The Odin Project](https://www.theodinproject.com/courses/foundations/#javascript-basics){target=_blank} or [The Modern JavaScript Tutorial](https://javascript.info/){target=_blank} to get the basics. Beyond basic JavaScript, students should be familiar with Node and npm. Some advanced students will also be using React in this course. Here are some resources to help familiarize yourself with these:

*   [The Odin Project: Introduction to Node](https://www.theodinproject.com/paths/full-stack-javascript/courses/nodejs){target=_blank}
*   [JavaScript Fundamentals Before Learning React](https://www.robinwieruch.de/javascript-fundamentals-react-requirements){target=_blank}

## Code Editor

[VSCode](https://code.visualstudio.com/download){target=_blank} is a very popular editor with developers due to the plug-ins and extensions it makes available. We would recommend getting started with it and the following plug-ins / features:

*   [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer){target=_blank} which allows you to easily start a server in the directory
*   [Live Share](https://visualstudio.microsoft.com/services/live-share/){target=_blank} an easy way to share your code with someone for pair programming
*   [Gitlens](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens){target=_blank} "supercharges the Git capabilities built into Visual Studio Code."
*   [Solidity Visual Developer](https://marketplace.visualstudio.com/items?itemName=tintinweb.solidity-visual-auditor){target=_blank} Built by ConsenSys!
*   [Solidity linter](https://marketplace.visualstudio.com/items?itemName=JuanBlanco.solidity){target=_blank} Checks valid Solidity syntax. Fair warning, can be over-opinionated for folks!
*   [Solidity Solhint](https://marketplace.visualstudio.com/items?itemName=idrabenia.solidity-solhint){target=_blank}
*   [Partial Diff](https://marketplace.visualstudio.com/items?itemName=ryu1kn.partial-diff){target=_blank} Compare (diff) text selections within a file, across files, or to the clipboard
*   [Markdown All in One](https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one){target=_blank} All you need to write Markdown
*   [GitHub Linker](https://marketplace.visualstudio.com/items?itemName=gimenete.github-linker){target=_blank} Create links to fragments of code in GitHub

We strongly recommend using VSCode in this course, particularly if you're new to coding, due to its extensive plugins. Other popular editors include [Atom,](https://atom.io/){target=_blank} [Sublime Text,](https://www.sublimetext.com/){target=_blank} and [IDEA](https://www.jetbrains.com/idea/){target=_blank} (written originally for Java but now supports many languages).

There is also the option of text-only editors. Many developers find them extremely productive and, while challenging to learn, make their job much easier. We'll address one here, vim, by providing this series of tutorials:

*   [History and Effective Use of Vim](https://begriffs.com/posts/2019-07-19-history-use-vim.html){target=_blank}
*   [Vim for Beginners](https://thevaluable.dev/vim-beginner/){target=_blank}
*   [Vim for Intermediate Users](https://thevaluable.dev/vim-intermediate/){target=_blank}
*   [Vim for Advanced Users](https://thevaluable.dev/vim-advanced/){target=_blank}

If you'll be using text-only editors, or simply using the command line for your development environment, you'll want to get familiar with `tmux`: [Getting Started with Tmux](https://sunainapai.in/blog/get-started-with-tmux/){target=_blank}
