This is a nicely formulated and stimulating question. The answer of course is ["Mu"](http://c2.com/cgi-bin/wiki?MuAnswer). The comment of István Zachar is among those lines...
(Here is the official ["Mu"](https://en.wikipedia.org/wiki/Mu_(negative)#The_Mu-koan) link.)

Usually when we cannot answer a question in the terms it is asked we extend the paradigm. 
(E.g. coming up with complex numbers. Or getting enlightened. Or bringing straw men.) 
So, what follows is my view of how the opposed in the question perspectives can be resolved. 
For simplicity of the explanations I both over-simplify and over-exaggerate.

The names "Leonid" and "Mr. Wizard" are used to designate code producing agents as described in the question. 
Those names should not be seen as literal references to the programming activities of the corresponding persons.


## Diagnosing the dichotomy

1. In Object-Oriented Programming (OOP) languages the key concept is reuse. We do not want to have the domino effect when changing parts of the code because of new understanding of the problem domain the code operates in. 
That is why we encapsulate behavior in objects, etc. We can say that modeling in OOP is with an entity centric language: the entities are objects and they exchange messages. 
Leonid's breakdown of functions can be seen to come from similar considerations (with a structural programming flavor). 

2. In Functional Programming (FP) languages we have the ability -- and we are enticed -- to refine our code iteratively until we derive essentially a new language that fits the problem domain of our code. FP provides modeling with a verb centric language. The valency of the verbs can be used to make new verbs, etc. Fundamental understanding of the problem domain brings the derivation of new verbs. Mr. Wizard's coding style comes from that perspective.

3. A person would prefer one or the other approach based on person's native language and scientific, engineering, or mathematical background and the audience. For example, chemists would prefer OOP (and flow charts) because they study processes of matter changing states. A mathematician might select different styles when communicating through code to (i) other mathematicians in academia, or (ii) software engineers in large companies.
 
4. The two approaches should not be just contrasted but seen as dual. For example, consider a graph G in which the nodes are entities and the edges are messages exchanged by the entities. This graph corresponds to OOP. Now consider the [line graph](https://en.wikipedia.org/wiki/Line_graph) L(G) in which the edges of G become nodes and the nodes of G become edges. That L(G) graph corresponds to FP. 

5. Leonid does FP by using L(G) i.e. by seeing functions as objects. Mr. Wizard does FP using G but seeing edge paths not vertices and links between them.

## Proposed cure

One way to address the opposing forces of the two perspectives is to factor out the reuse concern from the brevity and simplicity of implementation concern. 

One way do this is to have a Domain Specific Language (DSL) that is easy to use and understand. 
Say, a DSL close to the natural language of the intended users. 
The DSL will bring what Leonid wants, the interpreter of the DSL would bring code what Mr. Wizard wants. 
(And if done right Mr. Wizard might enjoy reading it.)

This can be facilitated with different tools. 
Below I demonstrate the use of [Functional Parsers](https://mathematicaforprediction.wordpress.com/2014/02/13/natural-language-processing-with-functional-parsers/) and the OOP Design Pattern [Interpreter](https://en.wikipedia.org/wiki/Interpreter_pattern).

The code in [this answer of mine](http://mathematica.stackexchange.com/a/114846/34008) illustrates fairly well "a DSL close to the natural language of the intended users" for programming tasks.

## Example

Below is (another) simple example that shows separated and reusable formulation in Leonid's manner, and coding in Mr. Wizard's manner. 
(Also see [this answer of mine](http://mathematica.stackexchange.com/a/110129/34008) about DSLs design and application in Mathematica.)

- The coding style of Leonid is used to come up with the EBNF grammar.

- The coding style of Mr. Wizard is used in both the EBNF grammar rules formulation and under the hood of the parser generation implementation. 
For the former see the functions applied at the end of some of the grammar rules, after the characters "<@". 
For the latter see the article ["Functional Parsers" by Fokker](http://www.staff.science.uu.nl/~fokke101/article/parsers/) -- it is exactly in the style Mr. Wizard likes. 
(My implementation [FunctionalParsers.m](https://github.com/antononcube/MathematicaForPrediction/blob/master/FunctionalParsers.m) is messier since it was written with an older Mathematica version.)

[![enter image description here][1]][1]

To be clear, this example shows that the two approaches can be both used by a higher abstraction layer. Mr. Wizard's approach can be tucked in into an interpreter and Leonid's approach would require users to program with clear natural language commands that can be decomposed into/within context free grammars. 
Mr. Wizard's approach facilitates the parsing and interpretation of those grammars, but otherwise is not visible to the users. 

## Conclusion

From the above it is clear that with the right attitude, automated tools, and smart computers Mr. Wizard's perspective becomes obsolete to humans, and Leonid's perspective endures, it bubbles up to the end users.

(Sorry if this conclusion seems too pessimistic. In my defense we increasingly live in a world that is all about outsourcing, offshoring, automation, and "the robots are coming"...)



  [1]: http://i.stack.imgur.com/kZswq.png

