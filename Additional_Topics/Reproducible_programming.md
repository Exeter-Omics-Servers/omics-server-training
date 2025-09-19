# Reproducible Programming

## Prerequisites

Participants must be familiar with the programming language chosen by the
instructor. This could be R, python, C, or even just some shell like bash.

Version control and GitHub knowledge might be useful if such content is
tackled.

## Learning Objectives

### Novice

By the end, novice partipants should be able to:

- Know what a linter is
- Know what a formatter is
- Understand how to specify software requirements
    - This has huge overlap with dependency management
- Create a plan for any software they intend to develop in the future
- Know how to make their software easy to use and collaborate on
- Name some test types and when they might use them

### Advanced

Some partipants may whiz through content. Such partipants can be directed to
learn about:

- How to setup linters and formatters in a workflow via GitHub actions (CI/CD)

## Proposed activities

### Style guides and formatting

Now following a style guide isn't a requirement (though it does make your code
more in line with what is seen in industry) unless you are submitting code to
a repository (like bioconductor for example). That being said, you should at
least have consistency within a codebase. You can show this quite easily with
a shell script where the variables all have different case styles and the
indentation is all over the place. Make it as hard as possible to read.

Formatting is often ignored as it is 'difficult to do', this is true if you do
all formatting manually. However formatters exist for the vast majority of
languages:

- Python -> ruff
- Anything web related -> Prettier
- C/C++ -> clang-tidy (clangd)
- R -> air

This can be delivered in parallel with linters as the two really go hand in
hand.

### Readme, installation instructions and documentation

Users can reflect on past experiences where they found it difficult to rerun
some analysis conducted by someone else, install a piece of software or even
a scenario where some instructions were unclear. What would they do
differently if they were the one writing these documents? This should be a
group discussion (split participants into smaller groups depending on counts).

### Improve code together

There's a lot of code out there (even in highly used repostories) that is
written very poorly. This is particularly true with many research outputs due
to time constraints, lack of training and lack of team cohesion. A fun exercise
might be to critique some code and having an open discussion on how to make it
better. For example, there is a repository with over 100 stars
on GitHub and thousands of downloads a month. I took the liberty of chucking
a bunch of poor code samples into generative AI to obtain this slop.

The exercise could center around all of the poor choices in the code (comments
removed of course):

- What is wrong with this code?
- How could it be improved?
- What could be done to avoid this kind of code being written in the future?

```R
# File: process_biological_data.R
# Purpose: Does some important biological stuff (probably)

MainProcessFunction <- function(File_location, outputfile) {
  
  theData = read.file(File_location)  # Inconsistent naming & no validation
  
  # 1. Hard-coded values & magic numbers
  theData = theData[theData$p < 0.05, ] 
  theData = theData[theData$confidence > 0.8, ]
  
  # 2. Redundant and confusing boolean check
  check_is_good = TRUE
  if (!isFALSE(check_is_good)) { 
    print("The check passed... somehow?")
  }
  
  # 3. Deeply nested logic (The "Arrowhead of Doom")
  if (!is.null(theData)) {
    if ("chr" %in% names(theData)) {
      for (i in 1:nrow(theData)) {
        if (!is.na(theData$pos[i])) {
          if (theData$pos[i] > 0) {
            theData$pos[i] <- theData$pos[i] + 1000000 # Magic number!
          } else {
            warning("problem at row ", i)
          }
        }
      }
    } else {
      stop("no chr col")
    }
  }
  
  # 4. Long function continues: mixing I/O with data manipulation
  final_output <- theData
  write.csv(final_output, file = outputfile)
  
  return(final_output)
}
```

### Testing

Some testing framework can be showcased to the participants that fits well with
the languages they are comfortable in. For example:

- Python users might want to look at pytest
- R users should use testthat (official framework)

If the instructor doesn't want to harper on about the specifics of a test 
framework, they could instead just go over a simple function and promote a
discussion on what kinds of unit tests one could write for it. Lots of
functions could be given out so that pairs or small groups could each work
on a different function.

### Software design and planning

When you write an essay (or any document really) you likely make a plan or
rough sketch first (or at least you should). The same thing goes for software.
It is ill-advised to dive straight into the deep end and attempt to write some
software in one shot if it is substantial or longer than 100-200 lines total.

Go over some techniques in how to plan out software. One possible approach for
this would be a tutorial where software is stripped out into modules that
all connect via one central backbone. This way, it is only the backbone one
needs to worry about when designing the software as the remaining modules
should be inherently orthogonal.

Contract based programming can also be a very helpful approach when designing
software (especially so with OOP languages).

Orthogonality is a big talking point here as well. A discussion can be brought
up/fabricated by showing paritcularly entangled software. Perhaps a 3 functions
all massively depend on the output of one another and so changing any one of
them warrants changing all 3. It is easy to ramp this up to showcase how
non-orthogonal programs end up eating into the programmer's time making such
spaghetti code annoying to deal with and uneconomic.
