# Gnu/Linux and shell scripting

## Prerequisites

Partipants must be able to have access to some POSIX compliant system with a
shell that is somewhat close to bash (for example, sh, zsh, dash).

- OSX users should be able to work with iterm (which uses zsh by default)
- Windows users are a little more tricky there are several options
    - WSL -> Can be intimidating to set up for some partipants
    - Git Bash -> Easy to install, won't have all features but basic shell
    operations are possible
    - Powershell is too dissimilar to bash to be used here
- ChromeOS users hopefully don't exist
- Other users probably won't need to be on this course

## Learning Objectives

### Novice

By the end, novice partipants should be able to:

- Explain what GNU/Linux is and why it is commonly used on HPC servers
- Explain the basics of the Linux file hierarchy structure standard (FHS)
- Navigate/Interact with the file system with ease (using `cd`, `mkdir`, `ls`,
`cat` *etc.*)
- Explain what is meant by the `PATH` environment variable
- Create basic shell scripts with:
    - Control flow
    - Variables
    - user input (`read` or command line arguments)
- Explain the basics behind the permissions system and how to interact with it
- Use a simple text editor like nano
    - Some partipants may prefer vi, vim, emacs or some other terminal text
    editor

### Intermediate

By the end, intermediate partipants should be able to:

- Know some basic GNU core utils (`awk`, `find`, `sed`, *etc.*)
- Know what a 'man' page is and how to access and read them
- Understand terms like 'kernel', 'userspace', 'shell' (*etc.*)
- Explain what an 'rc' file is
- Create personal aliases and functions
- Know about pattern matching characters (such as wildcard `*`)
- Understand IO streams

### Advanced

Some partipants may whiz through content. Such partipants can be directed to
learn about:

- Brace expansion (and similar)
- Traps and signals
- Lesser known GNU core utils
- File transfer with SCP, Rsync (*etc.*)
- Remaining enivronment variables
- Running process monitoring with `ps`, `top`, `pgrep` (*etc.*)

## Proposed activities

### Guided Lecture

Lectures are boring, but it is hard to provide an exercise to get participants
to learn about the core principles of GNU/Linux. Lecturing can be supplemented
with short tasks, for example:

- If explaining some topic, leave a gap and get participants to use the
internet to fill said gap in.
    - *e.g.* whilst explaining GNU/Linux, ask participants who the key
    contributors to the project are
- Encourage partipants to check if what you are saying is true
    - *e.g* for permissions, get them to use `sudo` to play around with the
    permissions of some file (can they read it? can they write to it? can they
    execute it? who can/cannot?)
- Use games to aid in understanding and remembering
    - *e.g.* a game of "taboo" might be fun. Participants can split into teams
    and each team must describe terms from the course without using certain
    words.

### Directory navigation task

Participants will use basic directory navigation to 'hide' a file with some
secret message on their system. After xxx minutes, partipants will swap 
machines and attempt to find this message in thier partner's web of
directories.

This encourages the use of: `mkdir`, `cd`, `echo`/`nano`, `cat`, `ls`

At the end one can show off `find` to trivialise the process

### Basic shell scripting

Participants can create a shell script (using their text editor of choice) that
could do the following:

- Asks the user for their name
- Print the name to standard output
- If the name is too long, print something different
- If the name appears in a blacklist file, print something different
- Use a loop for input validation
- *etc.*

The task can be anything, ideally something customisable to allow the
participant to explore the functionality on their own. Ideally participants can
lead this task whilst the instructor is there to help those that are stuck or
confused.

This encourages learning control flow, variables and user input

### File manipulation

Tailor some file manipulation task that fits in well with what partipants might
normally encounter in their research. For example:

- `awk` can be useful with tabular datasets (columnar operations, row/column
selection *etc.*).
    - Selecting only columns of interest from a UCSC BED file
- `grep` can be useful when finding text across multiple files
    - An rsid in a bim file
- `sort` might be useful when finding the largest value in a text file
    - The highest 'score' in a UCSC BED file
- `|`/pipes can be useful when combining the above commands (and will likely
come up naturally)

