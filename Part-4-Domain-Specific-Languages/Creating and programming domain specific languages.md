
## Introduction

In this chapter are given links to documents, packages, blog posts, and discussions for creating and utilizing Domain Specific Languages (DSL's). 
A few DSL's are discussed in the other chapters of this book part. 
This chapter provides a more general, higher level view on the application and creation of DSL's. 
The concrete examples are with WL, but the steps are general and can be done with any programming languages and tools.

## When to apply DSL's

Here are some situations for applying DSLs.

1. When designing conversational engines.

2. When there are too many usage scenarios and tuning options for the developed algorithms.

   * For example, we have a bunch of search, recommendation, and interaction algorithms for a dating site. 
   A different, User Experience Department (UED) designs interactive user interfaces for these algorithms. 
   We make a natural language DSL that invokes the different algorithms according to specified outcomes. 
   With that DSL the different designs produced by UED are much more easily prototyped, implemented, or fleshed out. 
   The DSL also gives to UED easier to understand view on the functionalities provided by the algorithms.

3. When designing an API for a collection of algorithms.

   * Just designing a DSL can bring clarity of what signatures should be in the API.

   * `NIntegrate`'s `Method` option was designed and implemented using a DSL. See [this video](http://www.wolfram.com/broadcast/video.php?c=400&v=1470) between 25:00 and 27:30.

   * See [this answer](http://mathematica.stackexchange.com/a/111919/34008) of the discussion ["Writing functions with “Method” options"](http://mathematica.stackexchange.com/questions/111666/writing-functions-with-method-options).

## Designing a DSL

1. Decide what kind of sentences the DSL is going to have.

   * Are natural language sentences going to be used? 

   * Are the language words known beforehand or not?
	

2. Prepare, create, or accumulate a list of representative sentences.

   * In some cases using [Morphological Analysis](https://en.wikipedia.org/wiki/Morphological_analysis_(problem-solving)) can greatly help for coming up with use cases and the corresponding sentences.   	


3. Create a context free grammar that describes the sentences from the previous step. (Or a large subset of them.)

   * At this stage I use exclusively [Extended Backus-Naur Form (EBNF)](https://en.wikipedia.org/wiki/Extended_Backus–Naur_Form).


4. Program parser(s) for the grammar.

   * I use most of the time [functional parsers](https://en.wikipedia.org/wiki/Parser_combinator).

   * The package [FunctionalParsers.m](https://github.com/antononcube/MathematicaForPrediction/blob/master/FunctionalParsers.m) provides a *Mathematica* implementation of this kind of parsing.

   * The package can automatically generate parsers from a grammar given in EBNF. (See the coding example below.)

   * I have programmed versions of this package in [R](https://github.com/antononcube/MathematicaForPrediction/blob/master/R/FunctionalParsers/FunctionalParsers.R) and [Lua](https://github.com/antononcube/MathematicaForPrediction/tree/master/Lua/FunctionalParsers).

5. Program an interpreter for the parsed sentences. 

   * At this stage the parsed sentences are hooked to the algorithms of the problem domain.

   * The package [FunctionalParsers.m](https://github.com/antononcube/MathematicaForPrediction/blob/master/FunctionalParsers.m) allows this to be done fairly easy.


6. Test the parsing and interpretation.

See the code example below illustrating steps 3-6.


## Introduction to using DSLs in Mathematica

1. This blog post ["Natural language processing with functional parsers"](https://mathematicaforprediction.wordpress.com/2014/02/13/natural-language-processing-with-functional-parsers/) gives an introduction to the DSL application in Mathematica.

2. This detailed slide-show presentation ["Functional parsers for an integration requests language grammar"](https://github.com/antononcube/MathematicaForPrediction/blob/master/Documentation/Functional%20parsers%20for%20an%20integration%20requests%20language%20grammar.pdf) shows how to use the package [FunctionalParsers.m](https://github.com/antononcube/MathematicaForPrediction/blob/master/FunctionalParsers.m) over a small grammar.


## Advanced example

The blog post ["Simple time series conversational engine"](https://mathematicaforprediction.wordpress.com/2014/11/29/simple-time-series-conversational-engine/) discusses the creation (design and programming) of a simple conversational engine for time series analysis (data loading, finding outliers and trends.)

Here is a movie demonstrating that conversational engine: [http://youtu.be/wlZ5ANglVI4](http://youtu.be/wlZ5ANglVI4).


## Other discussions

1. [This answer](http://mathematica.stackexchange.com/questions/111296/how-to-parse-a-clojure-expression/111321#111321) to the question ["How to parse a clojure expression?"](http://mathematica.stackexchange.com/questions/111296/how-to-parse-a-clojure-expression/) provides two concise examples of programming and/or generating parsers for a small grammar.

2. A small part, from 17:30 to 21:00, of the WTC 2012 ["Spatial Access Methods and Route Finding"](http://www.wolfram.com/broadcast/video.php?sx=Spatial%20Access%20Methods%20and%20Route%20Finding&v=35) presentation shows a DSL for points of interest queries.

3. The [answer](http://mathematica.stackexchange.com/questions/49052/css-selectors-for-symbolic-xml/49053#49053) of the MSE question ["CSS Selectors for Symbolic XML"](http://mathematica.stackexchange.com/questions/49052/css-selectors-for-symbolic-xml) uses [FunctionalParsers.m](https://github.com/antononcube/MathematicaForPrediction/blob/master/FunctionalParsers.m).


## Coding example

This example is for the steps 3-6 of the second section.

Load the package:

     Import["https://raw.githubusercontent.com/antononcube/MathematicaForPrediction/master/FunctionalParsers.m"]

Give an EBNF description of a DSL for food cravings:

    ebnfCode = "
      <lovefood> = <subject> , <loveverb> , <object-spec> <@ LoveFood[Flatten[#]]& ;
      <loveverb> = ( 'love' | 'crave' | 'demand' ) <@ LoveType ;
      <object-spec> = ( <object-list> | <object> | <objects> | <objects-mult> ) <@ LoveObjects[Flatten[{#}]]& ;
      <subject> = 'i' | 'we' | 'you' <@ Who ; 
      <object> = 'sushi' | [ 'a' ] , 'chocolate' | 'milk' | [ 'an' ] , 'ice' , 'cream' | 'a' , 'tangerine' ;
      <objects> = 'sushi' | 'chocolates' | 'milks' | 'ice' , 'creams' | 'ice-creams' | 'tangerines' ; 
      <objects-mult> = 'Range[2,100]' , <objects> <@ Mult ;
      <object-list> = ( <object> | <objects> | <objects-mult> ) , { 'and' &> ( <object> | <objects> | <objects-mult> ) } ; ";

Generate parses from EBNF string:

    GenerateParsersFromEBNF[ToTokens@ebnfCode];

Test the parser `pLOVEFOOD` for the highest level rule ( <lovefood> ) with a list of sentences:

    sentences = {"I love milk", "We demand 2 ice creams", 
      "I crave 2 ice creams and 5 chocolates", 
      "You crave chocolate and milk"}; ParsingTestTable[pLOVEFOOD, 
     ToLowerCase@sentences, "Layout" -> "Horizontal"]

[![enter image description here][1]][1]

Note the EBNF rule wrappers -- those are symbols specified at the ends of some of the rules. 

Next we implement interpreters. I am using `WolframAlpha` to get the calories. I gave up figuring out how to use `EntityValue["Food",___]`, etc. (Since using `WolframAlpha` is slow it can be overridden inside `Block`.)


    LoveObjectsCalories[parsed_] :=
      Block[{res, wares(*, WolframAlpha={}&*)},
        res = (StringJoin @@ 
              Flatten[Riffle[parsed, " and "] /. 
                Mult[{x_, y_}] :> (StringJoin @@ 
                   Riffle[Flatten[{ToString[x], y}], " "])]);
         wares = WolframAlpha[res <> " calories", "DataRules"];
          {{"Result", 1}, "ComputableData"} /. wares 
            /. {{"Result", 1}, "ComputableData"} -> 
             Quantity[RandomInteger[{20, 1200}], "LargeCalories"]
       ];

    LoveFoodCalories[parsed_] :=
      Block[{who, type},
       who = Cases[parsed, Who[id_] :> id, \[Infinity]][[1]];
       type = Cases[parsed, LoveType[id_] :> id, \[Infinity]][[1]];
       Which[
        who == "you",
        Row[{"No, I do not. I am a machine."}],
        type == "love",
        Row[{"you gain ", Sqrt[1*10.] parsed[[-1]], " per day"}],
        True,
        Row[{"you will gain ", parsed[[-1]]}]
       ]
      ];

Here the parsing tests are done by changing the definitions of the wrapping symbols `LoveFood` and `LoveObjects`:

    Block[{LoveFood = LoveFoodCalories, LoveObjects = LoveObjectsCalories},
     ParsingTestTable[pLOVEFOOD, ToLowerCase@sentences, "Layout" -> "Vertical"]
    ]

[![enter image description here][2]][2]


  [1]: http://i.stack.imgur.com/hreAy.png
  [2]: http://i.stack.imgur.com/xTmas.png

