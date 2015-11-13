config
======

A short explanation of the code QA measures and tools.

Android Lint
------------

Android specific lint.


Checkstyle
----------

Enforces coding style.

NOTE: using SuppressWarningsHolder annotations to suppress specific warnings


Findbugs
--------

Uses static analysis to find bugs in java code.

NOTE: to suppress warnings we use the two annotation libs to get that annotation feature among others.


JavaNCSS
--------

Measures Non Commenting Source Statements(NCSS), Cyclomatic Complexity Number(McCabe metric),  and
the number of formal javadoc comments per class and method. In other words measures how much
code we actually have.



JDepend
-------

Generates some design quality metrics that can be used to review and refactor code design and code
implementations. You do not use to get a certain level of metric value rather you use the metrics
produced to invert dependencies such that low-abstraction packages depend upon high-abstraction packages.


PMD
----

Java specific lint, enough said.

To Suppress:

```
@SuppressWarnings("PMD")
public class Bar {
 void bar() {
  int foo;
 }
}
@SuppressWarnings("PMD.UnusedLocalVariable")
public class Bar {
 void bar() {
  int foo;
 }
}

```
