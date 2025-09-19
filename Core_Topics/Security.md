# Security

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

By the end, novice participants should be able to:

- Explain what phishing and spear phishing are and why the latter is harder to
spot
- Explain the basics of linux permissions and how these can be used to protect
their data
- Understand the safe guards one has when downloading files from online onto
the server
    - Generally, package managers should keep you safe, but downloading
    software from a site and immeditately running it is generally a bad idea
    - checksums and GPG signing where possible
- Explain the possible dangers of using AI code in security critical contexts
    - Fine to use generative AI, just make sure you know what it is doing
    before running it
    ([prompt injection incident](https://www.malwarebytes.com/blog/news/2025/08/ai-browsers-could-leave-users-penniless-a-prompt-injection-warning))

### Intermediate

By the end, intermediate participants should be able to:

- Know how to check scripts that may be pulled from a repository online
    - For example, miniconda has a script that installs the program. Although
    this is safe for miniconda, lots of other software is installed like this
    and some of this may be malicious.

## Proposed activities

### Data breaches

Unless participants have never touched a computer before, it is basically
guaranteed that they have been in a data breach. This activity will showcase
how many times this has happened and whether or not any of their passwords have
been compromised.

This is a small script to obtain the SHA1 of your password securely:

```bash
echo -n "Please enter your password: " && read -rs pass
echo -n "${pass}" | openssl sha1 | awk '{print $2}'
unset pass
```

The above will read a password in without key strokes appearing on screen, the
password is then converted into its SHA1 hash and then immediately unset (so
as not to remain in the `env`).

Participants can then use the first 5 characters with haveibeenpwned.com's API.
From the list they can serach for a SHA1 match. If it exists, then they should
probably change that password if it is being used for anything important (as
even you, the instructor could obtain their credentials, nevermind a malicious
hacker).

[api](https://api.pwnedpasswords.com/range/)

The instructor could possible show a tutorial with 'password' and show how this
is objectively a terrible choice for a password.

haveibeenpwned.com also has a nice webapp that can show you which data breaches
a particular email account has been involved in. I (Sam Fletcher) have
personally been involved in over 80 with my throwaway Google mail account.

