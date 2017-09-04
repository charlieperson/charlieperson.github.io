---
layout: post
title: "Formatting"
date: 2017-07-28
---

If you've been a developer for any considerable amount of time, you've probably
experienced some amount of change. Perhaps the requirements of certain functionality,
specific technologies becoming deprecated, or maybe customer feedback has lead you
to pivot. Regardless, the code that we write today will ultimately change. Therefore,
we should write our code with modularity and extensibility in mind- however, that takes
experience and skill. Consistent formatting practices improve our code's readability
which, in turn, makes change less painful. Also, it doesn't take skill or experience-
it just takes discipline. Formatting truly is the low hanging fruit of creating well
designed systems.

### File size:
- Keep your files small. Of course, there are exceptions to every rule, but we should
start to think about refactoring as our files begin to push the 200 line mark.

### The Newspaper Metaphor:
- Our source files should be written like newspaper articles. In the same way that
a headline tells us what the article is about, our file names should be a clear indication
of what we are looking at, and if we're in the right place. The most high-level
concepts should be at the top and the details should increase as we make our way
down to the end of the file.

### Vertical Openness Between Concepts:
- Related concepts should be grouped together like paragraphs in an article. When
a new concept is introduced, we can and should cue the reader with white space.

### Vertical Distance:
- Closely related concepts should be close to each other vertically. If closely
related concepts are not grouped together, we can often find ourselves searching
for methods and scrolling down the page to find out where certain methods are, when
in reality, we shouldn't be wasting our time trying to figure our where things are,
but rather what they are doing.

### Variable Declarations:
- Variables should be defined at the top of our functions. An exception to this rule
is control variables for loops.

### Instance Variables:
- Instance variables should be at the top of our classes.

### Dependent Functions:
- If one function calls another, then they should be vertically close, and the
function that calls the other one should be above the one in which it is calling.

### Horizontal Formatting:
- No surprises here. Keep our lines short. 80 characters is standard, yet 100-120
can be okay. Anything past is often an indication of carelessness.

### Horizontal Alignment:
```
public    Date         date;
protected String       name;
private   String       modelID
private   int          age;
private   InputStream  input;
public    OutputStream out;
```
We should not do this because it tempts us to look at the variable names and not
the types, which is actually more important. If we are tempted to do this, it also
serves as an indication that we probably have more instance variables than we should
and might want to break

### Indentation:
It's crucial to maintain a hierarchical structure in our code with proper indentation.
This allows programmers to better follow the logic flow and avoid the noise of a program
by mentally segmenting out what is currently relevant. We should avoid one liners.

### Team Rules:
On a large project, it's important to establish a set formatting style at the beginning.
Personal formatting preferences are trumped by the team's standard.
