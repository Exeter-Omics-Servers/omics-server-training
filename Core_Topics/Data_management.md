# Data Management

## Prerequisites

Some tasks might warrant participants knowing the basics of GNU/Linux and
the syntax of markdown documents. Though this is completely up to the
instructor in how they choose to deliver the content.

## Learning Objectives

### Novice

By the end, novice participants should be able to:

- Articulate how their data management choices impact both their own work
and other users of the server
- Understand the importance of backups and how they might accomplish this
    - 3-2-1 principle
    - RDS buckets, source code respository hosting platforms (*etc.*)
- The importance of metadata in reproducibility
- Directory heirarchy design and file naming
    - This will likely differ between teams depending on their design
    philosophy
- Explain data life cycles
    - Understand why one might want to separate data into 'scratch space',
    active data and long-term archived data

### Intermediate

By the end, intermediate participants should be able to:

- Understand what a checksum is and how one can be used to verify the integrity
of a file (after a transfer for example)
- Automation of file operations (verification, downloads, renaming, moving
*etc.*)
- The differences between inode types on Linux and how they can best be used
    - Symlinks to reduce copies for example

## Proposed activities

It would appear that the general data management strategy for each server
differs slightly (not in core principles, more in actual implementation). As
a result, it might be beneficial to separate the partipants for this course
so content can focus on the actual implementation.

### Checksum/Integrity checking

Share some images in a tarchive with the participants. Participants can then
use checksum utilities (like `openssl`, `md5sum`) to check if any files are the
same. Then users can open said files to validate that the checksum information
does indeed show that two files are the same (well, not necessarily, but most
participants can ignore this).

Then users could open up one of these images as a text file to corrupt it.
After doing this they can then compute checksums to validate that some data
is indeed corrupted in the image (mismatch in checksums).

### Critique poor directory structure

Showcase some bad directory structure with terrible file naming choices. Get
partipants to discuss in groups what makes these choices poor and how they
might possibly resolve these issues.

### Create a README

Give partipants a directory that contains a bunch of data from some analysis
but provide no metadata describing it. Get participants to create a README
file for this dataset. This should hopefully drill in the idea that trying to
understand a bunch of unlabelled analysis is a huge pain and the burden should
not be placed on others.

### Automated data renaming/moving

Provide a bunch of text files (can be blank to save space) that need to be
renamed/moved. Perhaps every file contains the same prefix and this should
be removed such that `prefix_file_name.ext` is moved to `prefix/file_name.ext`.
Participants can do this manually for some, but will be quickly overwhelmed
with the number of files to change. Using some basic linux commands here will
help massively.

### Data lifecycle diagrams

Participants can be encouraged to think about a project they are currently on
and answer questions like:

- What data do they have?
- What data is most important?
- What data can be recreated?
- How should each bit of data be stored?

Participants can then also create a diagram showcasing the lifecycle of each
piece of data:

- How is it stored now?
- Where is the metadata and what does it include?
- Where will the data be next week? In 3 months? In 2 years?
