# Version Control

## Prerequisites

Partipants must be able to have access to some POSIX compliant system with a
shell that is somewhat close to bash (for example, sh, zsh, dash).

- OSX users should be able to work with iterm (which uses zsh by default)
- Windows users are a little more tricky there are several options
    - WSL -> Can be intimidating to set up for some users
    - Git Bash -> Easy to install, won't have all features but basic shell
    operations are possible
    - Powershell is too dissimilar to bash to be used here
- ChromeOS users hopefully don't exist
- Other users probably won't need to be on this course

partipants should also know the basics of GNU/Linux (at the very least be
comfortable navigating the file system and reading files).

## Learning Objectives

### Novice

By the end, novice partipants should be able to:

- Explain why one might want to use version control over simply labelling files
'V1','V2' (*etc.*)
- Understand the basic 'add commit' flow of git
- How to go 'back in time' (with commands like `checkout`, `restore`, `revert`,
`reset`)
- Understand the difference between git and GitHub
- Be able to use repository hosts like GitHub (`push`/`pull`)

### Intermediate

By the end, intermediate partipants should be able to:

- Understand what a merge conflict is, how it happens and how to resolve one
- Understand the infrastructure of git (staging area, working directory,
repositories)
- Understand branch switching, creation and deletion
    - And why you might want to use this feature
- Know what the `.gitignore` file does

### Advanced

Some partipants may whiz through content. Such partipants can be directed to
learn about:

- Rebasing (fixups, squashing, renaming *etc.*)
- Other version control systems (perhaps svn or jj)
- GitHub specifics like 
    - Workflows/Actions
    - Pull requests
    - Issues
    - Templates
    - Pages
    - Branch protection
    - Project boards
    - Milestones
- Submodules
- `git bisect`
- How git and other version control systems actually work (hard)
    - Blob and tree objects

## Proposed activities

### Simple git usage

Create a git repository
Make a text file, add and commit it
Change the text file, add and commit it
Revert a change

This is indeed simple, but the main thing here is getting participants
comfortable with the process.

### Merge conflicts

Create a branch and change the same line of a file on two branches, merge these
branches to create a merge conflict.
Participants should then be taught what the funny `<<<<<` `>>>>>>` `=====`
lines mean and subsequently how to resolve the conflict.

### Chatting in pairs

Using a GitHub repository that both partipants have access to, send messages to
one another via a text file on said repository. This follows nicely on from the
previous two activities but now introduces a repository host into the mix.
Participants can learn about pull requests and are much more likely to bump
into merge conflicts (as they will be continuously changing the same file on
separate branches, even if they are both on 'main').

## Non-activity based approach

If activity based learning doesn't seem feasible (or it just feels easier to
deliver the content in a 'tutorial' based manner) then this could be one such
approach:

### git

- Explain why version control is useful (no more `file.txt`, `file_new.txt`,
`file_final.txt`)
- `git init`
    - New users will probably get a warning about the branch name (master not
    main). This can be brushed aside, it really doesn't matter
- add a file and put some text in it
- `git add`, `git commit`
    - I'd recommend using `git commit -m` so there's no need to deal with
    configuration
    - New users will get a warning about setting username and email. This
    really doesn't matter and can be ignored. But I guess this can be covered
    briefly
- `git status` and `git log` to show git knows changes have been made and what
has been tracked
- make a couple more commits
- `git revert`, `git reset`, `git restore`, `git checkout` to 'edit' and move
about history
    - `git log`/`git status` will be very useful here in showing what is
    happening
    - Might want to ignore the bit about `HEAD` here that will come up when
    using `git checkout` to go back in history.

### GitHub

- Explain why GitHub is useful and how it is different to git (just a server to
hold git repositories (not files!))
- Create blank repo on GitHub
- Copy commands given to complete initial push of repo to GitHub
- Change file on GitHub
- Use `git pull` to retrieve changes
- Change file on GitHub and locally
    - Do this in a way that won't cause a merge conflict
- Try to `push` (failure due to unmerged local changes)
- `pull`, then `push` changes.
- Show branches (to help avoid problem just shown)
    - make new branch locally
    - make commit
    - open PR
    - merge online
    - `git switch` back to main
    - pull changes into your branch

### If time

- Manufacture merge conflict locally (but explain how the same applies when
collaborating)
    - Create a new branch
    - commit some change to a file
    - switch to main branch
    - commit some change (different) to the same file
    - use `git merge branch` and observe merge conflict message
    - Explain why conflict occurs
    - use `git status`
    - open file and show/explain `<<<<<` `>>>>>>` `=====` strings
    - Resolve conflict

## Alternative

Just copy what is done in the CFRR courses. The only caveat with this is that
the amount of content is meant to cover 6 hours (and still might not be
covered).
