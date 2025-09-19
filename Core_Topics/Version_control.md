# Version Control

## Prerequisites

Users must be able to have access to some POSIX compliant system with a shell
that is somewhat close to bash (for example, sh, zsh, dash).

- OSX users should be able to work with iterm (which uses zsh by default)
- Windows users are a little more tricky there are several options
    - WSL -> Can be intimidating to set up for some users
    - Git Bash -> Easy to install, won't have all features but basic shell
    operations are possible
    - Powershell is too dissimilar to bash to be used here
- ChromeOS users hopefully don't exist
- Other users probably won't need to be on this course

Users should also know the basics of GNU/Linux (at the very least be
comfortable navigating the file system and reading files).

## Learning Objectives

### Novice

By the end, novice users should be able to:

- Explain why one might want to use version control over simply labelling files
'V1','V2' (*etc.*)
- Understand the basic 'add commit' flow of git
- Understand the difference between git and GitHub
- Be able to use repository hosts like GitHub (`push`/`pull`)

### Intermediate

By the end, intermediate users should be able to:

- Understand what a merge conflict is, how it happens and how to resolve one
- Understand the infrastructure of git (staging area, working directory,
repositories)
- Understand branch switching, creation and deletion
    - And why you might want to use this feature
- Know what the `.gitignore` file does
- How to go 'back in time' (with things like `reset` and checking out to an 
older commit)

### Advanced

Some users may whiz through content. Such users can be directed to learn about:

- Rebasing (fixups, squashing, renaming *etc.*)
- Other version control systems (perhaps svn or jj)
- GitHub specifics like workflows, 
- Submodules
- `git bisect`
- How git and other version control systems actually work (hard)
    - Blob and tree objects

## Proposed activities

### Simple git usage

Create a git repository
Make a text file, add and commit it
Change the text file, add and commit it

This is indeed simple, but the main thing here is getting participants
comfortable with the process.

### Merge conflicts

Create a branch and change the same line of a file on two branches, merge these
branches to create a merge conflict.
Participants should then be taught what the 'funny <<<<< >>>>>> =====' lines
mean and subsequently how to resolve the conflict.

### Chatting in pairs

Using a GitHub repository that both users have access to, send messages to
one another via a text file on said repository. This follows nicely on from
the previous two activities but now introduces a repository host into the mix.
Participants can learn about pull requests and are much more likely to bump 
into merge conflicts (as they will be continuously changing the same file on
separate branches, even if they are both on 'main').
