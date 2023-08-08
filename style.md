# Code Style

This chapter summarizes hints specific to the code design and style.

Note: instead of _method_, the term _function_ is used here, because it is more generic. All
principles mentioned here apply to all programming paradigms, not just object-oriented programming (
where methods are used).

## Naming is essential

Probably the most important part of code design is naming. The better names you assign to the
variables, classes and functions, the easier it is to read the code. A good name conveys the meaning
of the code in an elegant way.

It is probably also the most difficult part (until you go
into [multi-threading](http://www.quickmeme.com/meme/364490)). It is simple to name things when you
work with cars, airplanes, bicycles, animals, squares, etc. But you rarely make zoo-games in real
life. In real life you will struggle with names such as `BusinessLogicBehaviorRepository`
and `PostRequestInterceptorFactory`. Nevertheless, assigning good names is one of the most important
tasks for a programmer.

Unfortunately, there are no clear rules on how to choose the names. There are only tips and
guidelines. Here are some tips based on my observations.

### Avoid Test1, MyTest, TestTest

Students quite often start exploring a new area with a test or two. They name things `test1`,
`test2`, `testA`, `testB`, etc. There is nothing wrong with experimenting. But you should never
include `test` in the name, unless it really is an automated test which will stay in your code base
as a regression test. There are at least two problems when using `test-` names:

1. You don't get into the habit of naming things right. If you don't at least try to name things
   correctly from the beginning, when will you try?
2. It is easy to forget to change things later, and there you are - you get `test` names in your
   production code. This looks very unprofessional.

### Avoid abbreviations

In the early days screens were tiny and there was little help from an editor. This meant that source
code had to be short. Therefore, programmers used short names for variables. These days are gone.
Let's not introduce confusion in the code by using unnecessarily short variable names!

If you have a function which returns a phone number, you should call it `getPhoneNumber`. You may
call it `getPhone`, but don't call it simply `pn`, or `getPhoNr`.

There are some classical short variables, such as variables `i` and `j` as a loop indexes. If you
have mathematical formulas, you may use `x` and `y`, or `pi`, etc.

Another rule for abbreviation: the more local the context of a variable, the shorter the name can
be. For example, a variable which is used only in a single function, can be shorter, because you
don't need to remember the meaning of it in another function. Meanwhile, variables which are used in
the whole class (the whole source code file) should have longer and hence more understandable names.

But in general - it is better to sacrifice some screen space in favor of more intuitive names.

### Explain the meaning

Although it is hard to give specific tips on how to name things, there is one principle you can
always use. Try to explain to a friend (or another team member) what this _thing_ does. If it is a
variable, what does it store? What does its value mean? If it is a function, what does it actually
DO? Does it return something or does it calculate something that changes state of the object?

An example. Let's suppose you have a function called `handlePhoneNumber`. Can you guess by its name
what it is doing? What does it actually do with the phone number? What does it return? Now suppose
you have the same function, but it named `getFormattedPhoneNumber`. It provides a much more clear
hint of operation. What if that function would be called `validatePhoneNumber`? A totally different
expectation, right? All three function names say that there will be something to do with phone
number, but `handle` is so general, you don't have a clue what it means.

### Good names instead of comments

Prefer longer and more describing variable names instead of writing comments. An example.

Bad:

```java
// Average salary
int a=calculateAverage(salaries);
```

Better:

```java
int averageSalary=calculateAverage(salaries);
```

### Follow the conventions

There are some typical conventions in programming. For example, for getting a simple value (and
typically NOT changing any state of the object, just getting the value), you have the _getter_
functions: `getName`, `getAge`, etc. You don't call them `fetchName`, or `passName`. _Fetch_
would give an impression that this name is fetched from somewhere - perhaps from a database, from a
file, or over the network somewhere. If you have a function which simply returns a `name`
variable, just call it `getName`, etc.

Similarly, the setter methods. Don't call it `updateName` or `resetName`, call it `setName`, unless
you are really doing something more than just setting the value.

When you use specific frameworks or programming patterns, there are standard names. `Listener`,
`Event`, etc. Frameworks such as Spring have classes and/or interfaces such as `Repository`,
`Controller`, `Service`. Name your classes in accordance to the default patterns. How to know those
patterns? Study some [theory](attitude.md#study-theory-dont-just-try) ;)

## One responsibility per class and function

You have probably heard the principle of low coupling and high cohesion? Well, this tip is about the
cohesion or responsibility. You should divide your code so that every class and every function has a
single responsibility, at a single level. How do you know when it has too much responsibility? Try
to explain it to a friend (or yourself). If you use too many "and" words, it probably has too many
responsibilities.

Typical cases (code smells) when you want to split a function or class into two:

* Combining responsibilities at different levels. For example, business logic (calculations)
  and formatting in the same function (user interface).
* An "and word" in the name.
* The code of the function is longer than one screen (over 120 lines).
* Concepts of different levels are mixed. For example, comparing to HTML pages (high-level concept)
  and checking CSS classes of divs (low-level concept).
* You want to write a comment to explain the parts of a function. Perhaps it is better to split the
  function into several sub-functions?
* You start to insert empty lines to separate logically differing parts of the function.
* Too many local variables (or fields in a class) needed.

## Clean up before every commit

You should not leave cleanup for later. Rather, do small cleanup before every new commit into the
version control. In this way you will only commit clean code into your repository. It will always
look nice. Another benefit - instead of spending hours on one long and boring cleanup, you will
spend several portions of max 5min cleanups. This is psychologically much easier to do.

Remember to do the following before every commit:

* In case you have copied some code online (or from ChatGPT), add a reference to it. It is enough
  adding a comment "Code adapter from <sourceUrlHere>"
* Make sure you have correct package names. In case you copied whole files from somewhere, rename
  the packages, don't leave `com.example`, etc.
* Remove unused imports (top of the file).
* Update documentation and comments. In case you changed some logic, check if the comments are still
  relevant.
* Run [Checkstyle](https://checkstyle.sourceforge.io/)
  and [SonarLint](https://docs.sonarcloud.io/improving/sonarlint/), fix the issues they suggest.
  Most of their suggestions make sense.
* Fix indentation of the code.

## Folder and file naming

TODO - folder structure should make it clear what is found where
TODO - remove all temporary experimental code, don't store "project New", "project 2", etc.
TODO - if needed, create "experiments" or "sandbox" folder

## Get the dependencies right

TODO:

* Encapsulate logic
* Interchangeable UI and other "plugins" (I/O devices)

## Improve code structure by refactoring

TODO:

* Don't assume you get it right with the first try
* Refactor old names if these are not relevant anymore
* Consider changing structure instead of simply changing name
* Refactor regularly, in small chunks
* Careful with public methods and APIs
* Extract a method, give it a good name

## Use external tools

TODO - CheckStyle, SonarLint

## Set up proper indentation

TODO:

* Super important for readability. Bad indentation takes away attention.
* Set up auto-indentation
* Same rules for all developers
* Separate commits for indentation and style changes
* Use CheckStyle