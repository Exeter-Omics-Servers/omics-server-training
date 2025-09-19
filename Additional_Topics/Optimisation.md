# Optimisation

## Prerequisites

Participants must be familiar with the programming language chosen by the
instructor. This could be R, python, C, or even just some shell like bash.

This might need to go slightly lower level to fully describe why certain
choices are faster than others, so that background might be required.

## Learning Objectives

### Novice

By the end, novice partipants should be able to:

- Understand what profilers are avaialable and how to use them
- Know a handful of techniques to increase compute performance and decrease
memory usage
- Understand how to implement parallelism in their programming language of
choice

### Intermediate

By the end, intermediate partipants should be able to:

- Understand why certain choices in the code results in speed up/slow down
- Have a deeper understanding of how parallelism works and how to avoid issues
such as race conditions
- Explain the difference between concurrency and true parallelism
- Explain what short circuiting is

### Advanced

Some partipants may whiz through content. Such partipants can be directed to
learn about:

- The importance of cache warming in IO heavy benchmarking
- Additional techniques/tricks to eek out performance in their programming
language of choice
- Specialised algorithms for their use case

## Proposed activities

A classic example is to show the 'add numbers up to xxx' and showcase how
python may be slower than C, but loops are the enemy.

### R optimisation tips/tricks

I imagine most people will want to hear about R. Here, the main thing will
be eliminating loops from programs, using vectorised operations that `dplyr`
gives you and thinking about the algorithms being used. 

It is also useful to remove redundant logic from a program and to exclaim that
'your first idea usually is the worst idea'. These last two points work with
any programming language really.

The easiest way to showcase optimisation techniques is to show how fast each
program is (with/without optimisation) using some kind of profiler. At the base
level you have something like `time` (GNU). But if the instructor is looking
for something that shows a little more, they could consider using something
like [hyperfine](https://github.com/sharkdp/hyperfine). Hyperfine allows for
running multiple programs and comparing them easily as well as cache warming
(in case codes contain any IO operations).

Also there's the `Rprof()` function to profile the execution of R expressions
(or use `profvis` package for something more user friendly).

Some quick things to look into/explain to the group could be:
- ifelse vs if ... else ...
- Sorting algorithms (R has partial sorting algorithms as well when you just
want the top xxx)
- which based functions (which.min, which.max etc.)
- Using && over & for short circuiting
- The apply family
- matrices vs dataframes
- Packages -> tidyr, dplyr, data.table
- Maybe sparse matrices


The main activity could be to get everyone to produce a script that creates
a very large bed file and save it to disk:

```R
size <- 10000
max_start <- 1000000
df <- data.frame(
    "chr" = rep("chr1", size),
    "start" = floor(runif(size, 1, max_start))
    "end" = floor(runif(size, 1, max_start))
)
df[["name"]] <- vapply(
    1:size,
    paste(sample(LETTERS, 10), collapse=""),
    character(1)
)
write.table(
    df,
    file="file.tsv",
    sep="\t",
    col.names=FALSE,
    header=FALSE,
    row.names=FALSE
)
```

From here, we are going to do slow operations:

- Read this data in
- Add a new score column by using for loops
- if start is smaller than end then print start otherwise print end
- Iterate over the whole dataframe and pick out the max start value
- if both start and end are > xxx, then print the line

Then using some profiling, we can then do the faster approaches and prove they
are indeed faster:

- Read using `data.table` (if installed)
- use `dplyr` to add score column instead
- use `ifelse` instead of `if ... else ...`
    - Create a mask instead and then `which` over the mask
- use `which` to get max
    - use `which.max` for slight bonus speed
- Instead of nested ifs (or &) use && for short circuiting (and explain what
short circuiting means)

A big point in R is to just show that loops are the devil.

### Memory optimisation

Most users will only care about the speed in which a program completes and
so they will be focussed on the processing side of things. However, some users
might want to know how to work with exceedingly large datasets (which is
becoming more and more common). Techniques like partitioning, compression and
lazy loading can help dramatically over naive approaches.


Memory optimisation can also lead to performance increases too. At a simple
level one can explain how memory is tiered on a computer, with caches being
physically closest, RAM being further away and hard disks being even further
away. This obviously isn't the full picture and there is much more to it, but
physical distance is a good way of conveying this idea.

### Parallelism

Obviously people should be aware of parallelism. But just make sure people know
how and when to use this. It takes time to set up workers and so this isn't
always the best solution. Some problems require workers to communicate with
each other which (if done poorly) can lead to race conditions, deadlocks and
more.

In order to talk about parallelism, there needs to be an intoduction to how
computers work. We can just talk about CPUs here, but perhaps we can also talk
about memory transfers on a very high level as well.

This is why low level knowledge is specified in the prerequisites. This can
obviously be skipped if needs be.

An introduction to how to implement parallelism into code might be a better use
of time instead. The main thing that needs to taught would be the difference
between parallelism and concurrency (as a language like python for example has
the global interpretter lock, so spawning many threads doesn't actually achieve
parallelism at all).

### Calculating the sum of all integers 1 to n

This is a very simple task that participants can do. They can write a program
that sums all values from 1 to 10 million for example and return the answer
(depending on the language, integer overflow might need to be accounted for).
Hopefully participants attempt to do this with a for loop or a while loop (or
similar). Each participant can compare how fast their respective implementation
or language is at this task (with something like C beating other languages but
not by much). Perhaps some users know that you can use a `sum` function or
something like numpy to speed up the program.

This gets participants used to using command line profilers in the most basic
of contexts.

The real kicker being, a loop is a terrible algorithm choice. The sum of
numbers 1 to n can be calculated in nanoseconds/microseconds by using a
mathematical formula. This drives home the point that a better algorithm will
likely trump most other optimisations and often even parallelism.
