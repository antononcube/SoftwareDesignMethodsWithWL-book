# "Software Design Methods with Wolfram Language" book

This repository has chapters, code, and organizational materials for the book 
"Software Design Methods with Wolfram Language".

***The book is not finished yet -- it is a work in progress...***   

## In brief

The goal of this book is to show how to apply several popular methodologies for software design with Wolfram Language (WL).

WL is a general, multi-paradigm programming language. WL is mostly a functional programming language, but 
it also can be used in a procedural and Object-Oriented Programming (OOP) manner. 
Of course, since WL is functional it can be also easily used for the creation of Domain Specific Languages (DSL's). 

This book gives concrete directions how to do OOP, Monadic Programming, and DSL designs with WL. 
Concrete examples are presented and discussed.

The creation of call graphs and Universal Modeling Language (UML) diagrams is also discussed.

## Mission statement

This book primary goal is to give concrete technical guidance for the application and utilization in 
[WL](https://en.wikipedia.org/wiki/Wolfram_Language) 
of 
[OOP Design Patterns](https://en.wikipedia.org/wiki/Design_Patterns) and
[Monadic Programming](https://en.wikipedia.org/wiki/Monad_(functional_programming).
Additional goals are to give directions for making
[DSL's](https://en.wikipedia.org/wiki/Domain-specific_language)
and analyze code with code derived dependency graphs and UML diagrams.

## What to read?

Generally speaking, this book assumes a certain level of programming and mathematical maturity of the readers
and (post-beginner to) intermediate level mastery of WL.

Part 1, "Overview and general directions", overviews and discusses the relationships between the different
topics and material of this book. (This README file is the same as the "Overview" chapter. )

Part 2, "Object Oriented Programming Design Patterns", should be of interest to readers who know and have applied
OOP Design Patterns. For readers not familiar with OOP and Design Patterns it is better to skip Part 2.
The rest of the book -- Monadic Programming, DSL's, call graphs -- is largely independent of Part 2.

Part 3, "Monadic Programming", gives all theoretical knowledge and practical know-how to design and use software monads.
A good preliminary read for Part 3 is \[PW1\].

Part 4, "Domain Specific Languages", has a DSL making overview chapter that is an easy read. 
The rest of the Part 4 chapters are more technical.

Part 5, "Additional topics", has chapters that might be of general interest and although related
to the rest of the book largely independent from it.

Part 6, "Example applications", discusses non-trivial examples of utilizing OOP Design Patterns and Monadic Programming. 

Except Part 6 all other book parts can be read independently.

## Comparisons with other programming languages

The main parts of the book have (brief) comparisons with other programming languages.

[R](https://www.r-project.org) is the language used in most comparisons. 
In general, it is natural to compare R with WL over both OOP and Monadic Programming. 

## Code

### OOP Design patterns

The application and utilization of OOP Design Patterns in WL is given as a discipline to follow using the built-in
WL functionalities. I.e. without the support or facilitation of any additional code. 
(Other efforts to use OOP in WL do tend to use supporting code.)  

The application of OOP Design Patterns is exemplified with:
 
 - elements of [`NIntegrate`'s implementation](https://reference.wolfram.com/language/tutorial/NIntegrateOverview.html), and
   
 - the package ["GitHubDataObjects.m"](https://github.com/antononcube/MathematicaForPrediction/blob/master/Misc/GitHubDataObjects.m), [AAp2], (that should be compared with [AAp1].)

### Monadic Programming

The proposed style of Monadic Programming in WL is supported with the package 
["StateMonadCodeGenerator.m"](https://github.com/antononcube/MathematicaForPrediction/blob/master/MonadicProgramming/StateMonadCodeGenerator.m),
\[AAp3\], that allows monad code generation.

The package 
["MonadicTracing.m"](https://github.com/antononcube/MathematicaForPrediction/blob/master/MonadicProgramming/MonadicTracing.m),
\[AAp4\], demonstrates:
 
 - how to trace the execution of monad pipelines, and 
 
 - how to delegate the functionalities of a monad to another "decorating" monad. 

### DSL's

The making of DSL's is facilitated (to a point) with the package 
["FunctionalParsers.m"](https://github.com/antononcube/MathematicaForPrediction/blob/master/FunctionalParsers.m), 
\[AAp5\], that gives the ability to program or generate parsers for a wide variety of grammars. 
 
### Dependency graphs

WL's [reflection](https://en.wikipedia.org/wiki/Reflection_(computer_programming)
capabilities are utilized to facilitate the examination and analysis of WL code with:
 
- a package to make [Universal Modeling Language (UML)](https://en.wikipedia.org/wiki/Unified_Modeling_Language) 
diagrams, \[AAp6\], and   

- a package to make dependency call graphs, \[AAp7\].

## Videos

Below are given links to several videos with presentations that discuss the central topics in this book. 

- ["Object-Oriented Design Patterns"](https://www.youtube.com/watch?v=4Q6hOx63b08).

- ["Monadic Programming: With Application to Data Analysis, Machine Learning and Language Processing"](https://www.youtube.com/watch?v=_cIFA5GHF58).

- ["Voice-Grammar-Compute-Communicate: Take Control of Your Health Data"](https://www.youtube.com/watch?v=_rI1RxkeAcA).

## Additional comments

- More adequate titles for the book might be:

  - "Popular Software Design Methods with Wolfram Language", or

  - "Elements of Software Design using Wolfram Language".
 
- The current title can be used if book's contents is extended. (I have no plans for that though.)

- At this point I do not use OOP Design Patterns that often when programming in WL. 
This is largely because:
 
  - the "data science industry" increasingly relies more on the functional programming paradigm;
  
  - I program most of the time in R (and R has a nice OOP system);
  
  - the use of monadic programming provides a lot of the benefits of OOP Design Patterns.
   
- The first versions of most of the chapters were written as blog posts to 
[MathematicaForPrediction at WordPress](https://mathematicaforprediction.wordpress.com) or 
[MathematcaStackExchange](https://mathematica.stackexchange.com). 

## References

### OOP Design patterns related

[CA1] Christopher Alexander et al., The Oregon Experiment, Oxford University Press, 1975.

[CA2] Christopher Alexander et al., A Pattern Language - Towns, Buildings, Construction, Oxford University Press, 1977.

[CA3] Christopher Alexander, The Timeless Way of Building, Oxford University Press, 1979.

[GoF] Erich Gamma, Richard Helm, Ralph Johnson, John Vlissides, Design Patterns: Elements of Reusable Object-Oriented Software, Addison-Wesley, 1994.

[AAp1] Anton Antonov, 
[GitHubPlots Mathematica package](https://github.com/antononcube/MathematicaForPrediction/blob/master/Misc/GitHubPlots.m),
(2015), 
[MathematicaForPrediction at GitHub](https://github.com/antononcube/MathematicaForPrediction).

[AAp2] Anton Antonov, 
[GitHubObjects Mathematica package](https://github.com/antononcube/MathematicaForPrediction/blob/master/Misc/GitHubDataObjects.m),
(2015), 
[MathematicaForPrediction at GitHub](https://github.com/antononcube/MathematicaForPrediction).

### Monadic Programming related

[PW1] Philip Wadler, "The essence of functional programming", (1992), 
19'th Annual Symposium on Principles of Programming Languages, Albuquerque, New Mexico, January 1992.

[AAp3] Anton Antonov,
[State monad code generator Mathematica package](https://github.com/antononcube/MathematicaForPrediction/blob/master/MonadicProgramming/StateMonadCodeGenerator.m),
(2017),
[MathematicaForPrediction at GitHub](https://github.com/antononcube/MathematicaForPrediction).

[AAp4] Anton Antonov,
[Monadic tracing Mathematica package](https://github.com/antononcube/MathematicaForPrediction/blob/master/MonadicProgramming/MonadicTracing.m),
(2017),
[MathematicaForPrediction at GitHub](https://github.com/antononcube/MathematicaForPrediction).

### DSL making related

[AAp5] Anton Antonov,
[Functional parsers Mathematica package](https://github.com/antononcube/MathematicaForPrediction/blob/master/FunctionalParsers.m),
(2014),
[MathematicaForPrediction at GitHub](https://github.com/antononcube/MathematicaForPrediction).

### Code analysis related

[AAp6] Anton Antonov, 
[UML Diagram Generation Mathematica package](https://github.com/antononcube/MathematicaForPrediction/blob/master/Misc/UMLDiagramGeneration.m),
(2016),
[MathematicaForPrediction at GitHub](https://github.com/antononcube/MathematicaForPrediction).

[AAp7] Anton Antonov,
[Call graph generation for context functions Mathematica package](https://github.com/antononcube/MathematicaForPrediction/blob/master/Misc/CallGraph.m),
(2018),
[MathematicaForPrediction at GitHub](https://github.com/antononcube/MathematicaForPrediction).

 
-----
Anton Antonov   
Windermere, Florida, USA   
2019-07-27


