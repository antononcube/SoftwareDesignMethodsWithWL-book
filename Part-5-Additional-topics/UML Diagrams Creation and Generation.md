
## In brief

The goal of this chapter is to show how to create and generate 
[Unified Modeling Language (UML)](http://www.uml.org) 
diagrams in WL. It is closely related to the OOP Design Patterns chapters of Part 2.

## Package functions

This command imports the package 
["UMLDiagramGeneration.m"](https://github.com/antononcube/MathematicaForPrediction/blob/master/Misc/UMLDiagramGeneration.m) :

    Import["https://raw.githubusercontent.com/antononcube/MathematicaForPrediction/master/Misc/UMLDiagramGeneration.m"]

The package provides the functions `UMLClassNode` and `UMLClassGraph`. 

The function `UMLClassNode` has the signature

    UMLClassNode[classSymbol, opts]

`UMLClassNode` creates a `Grid` object with a class name and its methods for the specified class symbol. 
The option "Abstract" can be used to specify abstract class names and methods. 
The option "EntityColumn" can be used to turn on and off the explanations column.

The function `UMLClassGraph` that has the signature:

    UMLClassGraph[symbols, abstractMethodsPerSymbol, symbolAssociations, symbolAggregations, opts] 

`UMLClassGraph` creates an UML graph diagram for the specified symbols (representing classes) and their relationships. 
It takes as options the options of `UMLClassNode` and `Graph`.

## UML diagrams creation

Let us visualize a simple relationship between buildings, people, books, and a client program.

    UMLClassGraph[{Library \[DirectedEdge] Building, 
      Museum \[DirectedEdge] Building, 
      Member \[DirectedEdge] Person}, {}, {Library <-> Member, 
      Museum \[DirectedEdge] Member, Client \[DirectedEdge] Building, 
      Client \[DirectedEdge] Person}, {Library \[DirectedEdge] Book},
     "Abstract" -> {Building, Person},
     "EntityColumn" -> False, VertexLabelStyle -> "Text", 
     ImageSize -> Large, GraphLayout -> "LayeredDigraphEmbedding"]

![enter image description here][1]

In the diagram above the classes Person and Building are abstract (that is why are in italic). 
Member inherits Person, Library and Museum inherit Building. 
Library can contain (many) Book objects and it is associated with Member. Client associates with Building and Person.

## UML diagram generation

The main package function `UMLClassGraph` is capable of generating UML diagrams over Design Patterns code written in the style described in 
[Part 2](https://github.com/antononcube/SoftwareDesignMethodsWithWL-book/tree/master/Part-2-Object-Oriented-Programming-Design-Patterns).

Let us look into a simple UML generation example for the design pattern [Template Method](https://en.wikipedia.org/wiki/Template_method_pattern). 

Here is the WL code for that design pattern:

    Clear[AbstractClass, ConcreteOne, ConcreteTwo];
    
    CLASSHEAD = AbstractClass;
    AbstractClass[d_]["Data"[]] := d;
    AbstractClass[d_]["PrimitiveOperation1"[]] := d[[1]];
    AbstractClass[d_]["PrimitiveOperation2"[]] := d[[2]];
    AbstractClass[d_]["TemplateMethod"[]] :=
    CLASSHEAD[d]["PrimitiveOperation1"[]] + CLASSHEAD[d]["PrimitiveOperation2"[]]
    
    ConcreteOne[d_][s_] := Block[{CLASSHEAD = ConcreteOne}, AbstractClass[d][s]]
    ConcreteOne[d_]["PrimitiveOperation1"[]] := d[[1]];
    ConcreteOne[d_]["PrimitiveOperation2"[]] := d[[1]]*d[[2]];
    
    ConcreteTwo[d_][s_] := Block[{CLASSHEAD = ConcreteTwo}, AbstractClass[d][s]]
    ConcreteTwo[d_]["PrimitiveOperation1"[]] := d[[1]];
    ConcreteTwo[d_]["PrimitiveOperation2"[]] := d[[3]]^d[[2]];

This command generates an UML diagram over the code above:

    UMLClassGraph[{AbstractClass, ConcreteOne, 
      ConcreteTwo}, {AbstractClass -> {"PrimitiveOperation1", 
        "PrimitiveOperation2"}}, "Abstract" -> {AbstractClass}, 
     VertexLabelStyle -> "Subsubsection"]

![enter image description here][2]

Here is a diagram generated over a WL implementation of [Decorator](https://en.wikipedia.org/wiki/Decorator_pattern):

![enter image description here][3]

And here is a diagram for a concrete implementation of [Interpreter](https://en.wikipedia.org/wiki/Interpreter_pattern) for Boolean expressions:

![enter image description here][4]

(Interpreter is my favorite Design Pattern and I have made several WL implementations that facilitate and extend its application. 
See [Part 4](https://github.com/antononcube/SoftwareDesignMethodsWithWL-book/tree/master/Part-4-Domain-Specific-Languages).)


  [1]: http://community.wolfram.com//c/portal/getImageAttachment?filename=UML-diagram-for-Inheritance-Composition-Association.png&userId=143837
  [2]: http://community.wolfram.com//c/portal/getImageAttachment?filename=UML-diagram-generated-over-TemplateMethod-code.png&userId=143837
  [3]: http://community.wolfram.com//c/portal/getImageAttachment?filename=UML-diagram-for-Decorator.png&userId=143837
  [4]: http://community.wolfram.com//c/portal/getImageAttachment?filename=UML-diagram-for-Interpreter-of-BooleanExpr.png&userId=143837
