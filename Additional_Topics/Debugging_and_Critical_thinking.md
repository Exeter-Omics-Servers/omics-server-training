# Debugging and Critical Thinking

## Prerequisites

Participants must be familiar with the programming language chosen by the
instructor. This could be R, python, C, or even just some shell like bash.

## Learning Objectives

### Novice

By the end, novice partipants should be able to:

- Know what a linter is
- Be able to write a test under xxx framework
- Feel comfortable with debugging

### Intermediate

By the end, intermediate partipants should be able to:

- Be aware of some static code analysis programs and how to use them

### Advanced

Some partipants may whiz through content. Such partipants can be directed to
learn about:

- The debugging capabilities of their language of choice (beyond simple print
statements)
    - This could be the debug mode of the python interpreter or gdb for example

## Proposed activities

In the space of critical thinking and debugging, I (Sam Fletcher) have found
the following three avenues of thought incredibly useful:

1) Isolate the broken component. Often, the hardest part of debugging is finding
what is actually broken. 
 - Activities could focus on ways of isolating broken areas (debuggers are
 great for this, but print statements can work too if the instructor wants the
 course to be more accessible)
2) "Find the box". This mantra is my evolution of "Think outside of the box",
which I think is unhelpful. By "find the box", I want you to understand what
assumptions you have made (implicit and explicit).
    - This can be a hard habit to get into, but explaining what code does to
    another person or even writing it down on paper can help
    - Once you have "found the box" you can then test those assumptions (are
    any being violated?)
    - After evaluating the assumptions you can then change those assumptions
    or - in the case that they were implicit - actually enforce those
    assumptions in your code
3) Make the smallest possible case that breaks the program.
    - This one is more useful when you are debugging someone else's code rather
    than your own
    - This is synonymous with point 1). Effectively, you are isolating the
    broken component (just working in a different direction).

Activities that drill these into participants should prove highly valuable.
The simplest way to instill confidence in participant's ability to debug would
come in the form of debugging exercises (exposure).

### Python top 2 elements in unsorted list

So first you introduce the concept of finding a maximum value in a vector by
looping over the elements.

```python
def printMax(numbers):
    for number in numbers:
        if maximum < number:
            maximum = number
    print(f"maximum number is {maximum}")

printMax([5,3,2,10,1])
```

This has a syntax error in it. The interpretter will complain so the bug is
easy to spot. The problem being, `maximum` doesn't exist in the first loop run.
The fix might be:

```python
def printMax(numbers):
    maximum = numbers[0]
    for number in numbers:
        if maximum < number:
            maximum = number
    print(f"maximum number is {maximum}")

printMax([5,3,2,10,1])
```

This works great. But there's a problem, it breaks if there is no elements in
`numbers`. We might refer to this as a logical error. This problem arose
because we *assumed* that the vector had enough elements.

```python
def printMax(numbers):
    if not numbers:
        print("list is empty")
        return
    maximum = numbers[0]
    for number in numbers[1:]:
        if maximum < number:
            maximum = number
    print(f"maximum number is {maximum}")

printMax([])
```

Now lets expand this to get the first and second maximum (top two). Of course
we can sort the array, but this is slower (so we want to avoid this).

```python
def printTopTwo(numbers):
    if not numbers:
        print("list is empty")
        return
    maximum = numbers[0]
    second_maximum = numbers[1]
    for number in numbers[2:]:
        if maximum < number:
            maximum = number
        if second_maximum < number:
            second_maximum = number
    print(f"The top two numbers are {maximum} and {second_maximum}")

printMax([5,3,2,10,1])
```

This solution has multiple problems which are all logical errors:

- We should be checking if `numbers` has at least 2 values
- `maximum` and `second_maximum` might need to be switched
- The core loop does not work properly as `maximum` and `second_maximum` can
wind up being the same value

Some participant interaction can bring this activity a long way. Again, this is
just one example of some code. The important thing about this exercise is
getting participants to think about the ways they can break their code.
