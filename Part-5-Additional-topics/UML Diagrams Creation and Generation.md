This post is to show how to create and generate [Unified Modeling Language (UML)](http://www.uml.org) diagrams in *Mathematica*. It is related to programming in *Mathematica* using [Object-Oriented Design Patterns](http://www.wolfram.com/broadcast/video.php?c=400&v=1470).

## Package functions

This command imports the package [UMLDiagramGeneration.m](https://github.com/antononcube/MathematicaForPrediction/blob/master/Misc/UMLDiagramGeneration.m) :

    Import["https://raw.githubusercontent.com/antononcube/MathematicaForPrediction/master/Misc/UMLDiagramGeneration.m"]

The package provides the functions `UMLClassNode` and `UMLClassGraph`. 

The function `UMLClassNode` has the signature

    UMLClassNode[classSymbol, opts]

`UMLClassNode` creates a `Grid` object with a class name and its methods for the specified class symbol. The option "Abstact" can be used to specify abstract class names and methods. The option "EntityColumn" can be used to turn on and off the explanations column.

The function `UMLClassGraph` that has the signature:

    UMLClassGraph[symbols, abstractMethodsPerSymbol, symbolAssociations, symbolAggregations, opts] 

`UMLClassGraph` creates an UML graph diagram for the specified symbols (representing classes) and their relationships. It takes as options the options of UMLClassNode and Graph.

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

In the diagram above the classes Person and Building are abstract (that is why are in italic). Member inherits Person, Library and Museum inherit Building. Library can contain (many) Book objects and it is associated with Member. Client associates with Building and Person.

## UML diagram generation

The main package function `UMLClassGraph` is capable of generating UML diagrams over Design Patterns code written in the style exemplified and described in my [WTC 2015](https://www.wolfram.com/events/technology-conference/2015/) talk [Object-Oriented Design Patterns](http://www.wolfram.com/broadcast/video.php?c=400&v=1470).

Let us look into a simple UML generation example for the design pattern [Template Method](https://en.wikipedia.org/wiki/Template_method_pattern). 

Here is the *Mathematica* code for that design pattern:

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

Here is a diagram generated over a *Mathematica* implementation of [Decorator](https://en.wikipedia.org/wiki/Decorator_pattern):

![enter image description here][3]

And here is a diagram for a concrete implementation of [Interpreter](https://en.wikipedia.org/wiki/Interpreter_pattern) for Boolean expressions:

![enter image description here][4]

(Interpreter is my favorite Design Pattern and I have made several *Mathematica* implementations that facilitate and extend its application. See these blog posts of mine: ["Functional parsers" category in MathematicaForPrediction at WordPress](https://mathematicaforprediction.wordpress.com/category/functional-parsers/)).


  [1]: http://community.wolfram.com//c/portal/getImageAttachment?filename=UML-diagram-for-Inheritance-Composition-Association.png&userId=143837
  [2]: http://community.wolfram.com//c/portal/getImageAttachment?filename=UML-diagram-generated-over-TemplateMethod-code.png&userId=143837
  [3]: http://community.wolfram.com//c/portal/getImageAttachment?filename=UML-diagram-for-Decorator.png&userId=143837
  [4]: http://community.wolfram.com//c/portal/getImageAttachment?filename=UML-diagram-for-Interpreter-of-BooleanExpr.png&userId=143837
