# Typical Software Development Workflows 

--- 

## Dialectical Materialism perspective

> No, OOP is not fully Marxist
> But using Marx quotes in OOP papers / books seem always relevant


- The matter has objects

- The order between the objects (relative or absolute) gives the idea of space

- The second of events between the objects gives the idea of time

- Space and time give the idea of reality

- Nouns are assigned to object, verbs to events

- Nouns and verbs make language 

- The matter was first, the mind second

    - That is, actually, somewhat optional 

        - Not from DM POV, though

    - If the other way around, then a very complicated language exists used to create reality

------

## Top-down development (Structural Programming)


------

## Objects interchanging messages (in Object Oriented Programming)


- Which entities exchange what messages?

- What are the "hot spots" of the system?

- What is common, or invariant, or variable?

- Discovery of classes

    - Different types: analysis, design, and implementation

- Where the fundamental patterns apply?

    - Template Method and Strategy

- Where the second wave patterns apply?

    - Decorator, Composite, Freight, and others

- Which creation patterns apply?

    - Almost always, Builder and Abstract Factory

- Refine, rethink,  and program

    - Preliminary verbal descriptions and UML diagrams help

    - Yes, LLMs can be used over those to generate code

------

## Bottom-up development (in Functional Programming)

Masters of Functional Programming brainstorm while writing code and rewrite their code
until they get a reasonable Domain Specific Language (DSL) for the problem domain that code targets.

Here are the steps of that development workflow:

1. **Identify Complexity**: Recognize when a program component becomes too large and complex.
2. **Divide Program**: Break down the program into smaller, comprehensible parts.
3. **Apply Bottom-Up Design**: Develop new operators or utilities as needed to address specific problems.
4. **Integrate New Operators**: Use newly created operators to simplify and refine existing program components.
5. **Iterate and Evolve**: Continuously refine the language and program together, identifying patterns and opportunities for simplification.
6. **Promote Code Reuse**: Utilize utilities across multiple programs to reduce effort and increase efficiency.
7. **Simplify Program Structure**: Aim for a smaller, more abstract language with a concise program.
8. **Enhance Readability**: Ensure the program is easy to read by using general-purpose operators.
9. **Leverage Small Teams**: Utilize the productivity advantages of small teams in bottom-up design.
10. **Refinement Loop**: Revisit and refine components as new patterns and simplifications are identified.

Paul Graham says in [PG1]:

> In Lisp, you don’t just write your program down toward the language, 
> you also build the language up toward your program. As you’re writing 
> a program you may think “I wish Lisp had such-and-such an operator.” 
> So you go and write it.

----

## References

### Articles, books

[PG1] Paul Graham, On Lisp, (1993), Prentice Hall, ISBN-10: 0130305529, ISBN-13: 978-0130305527.