# "Software Design Methods with Wolfram Language" book

This repository has chapters, code, and organizational materials for the book 
"Software Design Methods with Wolfram Language".

***The book is not finished yet -- it is a work in progress...***   

## In brief

The goal of this book is to introduce several methodologies for software design with Wolfram Language (WL).

WL is a general, multi-paradigm programming language. WL is mostly a functional programming language, but 
it also can be used in an procedural and Object-Oriented Programming (OOP) manner. 
Of course, since WL is functional can be also used for the creation of Domain Specific Languages (DSL's). 

This book gives concrete directions how to do OOP, Monadic Programming, and DSL designs with WL. 
Concrete examples are presented and discussed.

## Mission statement

This book primary goal is to give concrete technical guidance for the application and utilization in 
[WL](https://en.wikipedia.org/wiki/Wolfram_Language) 
of 
[OOP Design Patterns](https://en.wikipedia.org/wiki/Design_Patterns),
[Monadic programming](https://en.wikipedia.org/wiki/Monad_(functional_programming).
Additional goals are to give directions for making
[DSL's](https://en.wikipedia.org/wiki/Domain-specific_language)
and analyze code with code derived dependency graphs and UML diagrams.

## Code

### OOP Design patterns

The application and utilization of OOP Design Patterns in WL is given as a discipline to follow using the built-in
WL functionalities. I.e. without the support or facilitation of any additional code. 
(In packages or otherwise, as seen in other effort to use OOP in WL.)  

The application of OOP Design Patterns is exemplified with:
 
 - elements of [`NIntegrate`'s implementation](https://reference.wolfram.com/language/tutorial/NIntegrateOverview.html), and
   
 - the package [AAp2] (that should be compared with [AAp1].)

### Monadic Programming

The proposed style of Monadic Programming in WL is supported with the package [AAp3] that allows monad code generation.

### DSL's

The making of DSL's is facilitated (to a point) with the package [AAp4] that gives the ability to program or generate
parsers for a wide variety of grammars.
 
### Dependency graphs

Using WL's reflexivity capabilities are utilized to facilitate the examination and analysis of code with:
 
- a package to make Universal Modeling Language (UML) diagrams, [AAp5], and   

- a package to make dependency call graphs, [AAp6].

## Videos

Below are given links to couple of videos with presentations of mine that discuss the central topics in this book. 

- ["Object-Oriented Design Patterns"](https://www.youtube.com/watch?v=4Q6hOx63b08).

- ["Monadic Programming: With Application to Data Analysis, Machine Learning and Language Processing"](https://www.youtube.com/watch?v=_cIFA5GHF58).

## Additional comments

- More adequate titles for the book might be:

  - "Popular Software Design Methods with Wolfram Language", or

  - "Elements of Software Design using Wolfram Language".
 
- The current title can be used if book's contents is extended. (I have no plans for that though.)

- At this point I do not use OOP Design Patterns that often when programming in WL. 
This is largely because:
 
  - the "data science industry" increasingly relies more on the functional programming paradigm;
  
  - I program in R (and R has a nice OOP system);
  
  - the use of monadic programming provides a lot of the benefits of OOP Design Patterns.
   
- The first versions of most of the chapters were written as blog posts to 
[MathematicaForPrediction at WordPress](https://mathematicaforprediction.wordpress.com) or 
[MathematcaStackExchange](https://mathematica.stackexchange.com). 

## References

### OOP Design pattern related

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

[AAp3] Anton Antonov,
[State monad code generator Mathematica package](https://github.com/antononcube/MathematicaForPrediction/blob/master/MonadicProgramming/StateMonadCodeGenerator.m),
(2017),
[MathematicaForPrediction at GitHub](https://github.com/antononcube/MathematicaForPrediction).

### DSL making related

[AAp4] Anton Antonov,
[Functional parsers Mathematica package](https://github.com/antononcube/MathematicaForPrediction/blob/master/FunctionalParsers.m),
(2014),
[MathematicaForPrediction at GitHub](https://github.com/antononcube/MathematicaForPrediction).

### Code analysis related

[AAp5] Anton Antonov, 
[UML Diagram Generation Mathematica package](https://github.com/antononcube/MathematicaForPrediction/blob/master/Misc/UMLDiagramGeneration.m),
(2016),
[MathematicaForPrediction at GitHub](https://github.com/antononcube/MathematicaForPrediction).

[AAp6] Anton Antonov,
[Call graph generation for context functions Mathematica package](https://github.com/antononcube/MathematicaForPrediction/blob/master/Misc/CallGraph.m),
(2018),
[MathematicaForPrediction at GitHub](https://github.com/antononcube/MathematicaForPrediction).

 
-----
Anton Antonov   
Windermere, Florida, USA   
2019-07-27


