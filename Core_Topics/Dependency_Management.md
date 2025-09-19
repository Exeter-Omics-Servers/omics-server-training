# Dependency Management

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

Partipants should also know the basics of GNU/Linux (at the very least be
comfortable navigating the file system and reading files).

Any software that is being used in the activities (miniconda for example).

## Learning Objectives

### Novice

By the end, novice partipants should be able to:

- Explain why one would want to use a dependency management tool and how it
can help with reproducibility
- Know how to use some dependency management tool that will prove useful in
their own work (it is likely conda will span most disciplines)

### Intermediate

By the end, intermediate partipants should be able to:

- If using conda, know about the license agreement that comes with using
packages hosted on anaconda repositories
    - And know how to change channels to avoid this if it affects them
    (conda-forge)
- How to point conda to a centralised packages directory to aid in caching and
reduce total space taken up by all users
    - either via `.condarc` or environment variables

### Advanced

Some partipants may whiz through content. Such partipants can be directed to
learn about:

- Look into how dependencies are resolved by such tools (hard)
    - DAG
- Look into other dependency management tools for other languages (spack, renv,
cargo *etc.*)

## Proposed activities

### Basic conda (miniconda/miniforge) usage

Participants will create a conda environment that uses either python version 2
or 3. They will then create a python script that only works with their version
(this code can just be given to participants, python knowledge isn't required).

Partipants can then export their environment to a text file (either via
`conda export` or `conda list -e`) to share with another participant. The other
user can now recreate the conda environment on their side. Participants can
swap scripts as well to show that the python script only works with the conda
environment that contains the correct python version.

This could be extended to include other software to emphasise that conda is
not just about storing which python version you are using.

This covers environments, their activation, installation of software and how
it can be useful in the context of reprocibility.

It would be even better if python3 was used in both scripts, but the minor
version difference leads to some bug (perhaps the use of the walrus operator
in python versions <3.8 and >=3.8).

### Annoying software dependencies

Have participants try to reconstruct a conda environment from a list of wonky
software specifications in an attempt to run some shell/R/python script. Once
they have a conda environment that is capable of running the script, they
should save this so that this tedious process doesn't need to be repeated by
others in the future.

This might be easier in python as you can write a script that can output error
messages saying the incorrect version of xxx package has been installed. 

The main problem with this task is that attempting to reinstall different
versions of packages over and over again can severally slow conda down.
Solutions would be to tell users they can start again from a clean install (or
use something that is much faster like pixi).

### Nextflow

Using Apptainer to run a simple nextflow pipeline (or perhaps just a nextflow
pipeline built in house that is extremally minimal). This would be more of a
tutorial for those users that see themselves using nextflow.
