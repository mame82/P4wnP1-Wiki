# Contributing
First of all: Thank you very much for thinking about contributing to the P4wnP1 project.
There are several tasks that need to be done, even some for people that are [not software developers](Other-Ways-to-Contribute.md).

Here are some places where you can find some suggestions:

* [P4wnP1 issue page](https://github.com/mame82/P4wnP1/issues)
* [Wiki issue page](https://github.com/mame82/P4wnP1-Wiki/issues)
* [The Wikis ToDo list](../ToDo.md)

## How do I contribute?
This depends on what you want to do:

### Contributing to the P4wnP1 code:
Contributions to the code follow the standard scheme for contributing:

* fork [the P4wnP1 Repository](https://github.com/MaMe82/P4wnP1).
* use `git clone https://github.com/<your username>/P4wnP1` _this won't clone the submodules required for running P4wnP1_
* setup the upstream repo so you can update your fork: `git remote add upstream https://github.com/MaMe82/P4wnP1`
* make a new branch `git checkout -b <desired name of the branch>`
* make your changes, add, and commit them.
* push them to your remote repository `git push upstream <name of your branch>`
* Clone your fork on the Pi and test your changes!
* PR them once you tested them thoroughly on github and hope they get merged.

### Contributing to the P4wnP1 Wiki:
Contributing to the wiki pretty much follows the same procedure as contributing to the code.
There is a pencil button at the top right of every page which will fork the wiki (if you are logged in) and allows you to edit that file.
Even though you will be able to edit the entire wiki in the github webinterface, you will need to clone your fork and install mkdocs if you want to test your changes since github will format the markdown differntly than mkdocs-material.

* Install git, python and pip
* (fork [the P4wnP1 Wiki](https://github.com/MaMe82/P4wnP1-Wiki)) you probably will have done that if you clicked the pencil in the wiki.
* use `git clone https://github.com/<your username>/P4wnP1-Wiki` to download the wiki into your current directory
* setup the upstream repo so you can update your fork: `git remote add upstream https://github.com/MaMe82/P4wnP1-Wiki`
* make a new branch `git checkout -b <desired name of the branch>`
* make your changes, add, and commit them.
* install mkdocs and depencies via `pip install mkdocs` and `pip install -r requirements.txt` while in the Wiki-Repository
* use `mkdocs serve` to build the doc and start the webserver.
* open your browser `127.0.0.1:8000` and review your changes.
* push them to your remote repository `git push upstream <name of your branch>` (be careful to exclude the site/ directory when adding your files for commit)
* PR them once you tested them thoroughly on github and hope they get merged.
