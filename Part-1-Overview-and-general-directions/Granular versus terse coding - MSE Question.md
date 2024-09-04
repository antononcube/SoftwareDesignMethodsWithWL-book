# Granular versus terse coding

While reading Leonid's grand answers to https://mathematica.stackexchange.com/questions/109888/general-strategies-to-write-big-code-in-mathematica/110001#110001 I came across something that goes against my own practices.  I do not disagree with the principle but the degree to which it is taken feels both alien and counterproductive to me.  Quite possibly Leonid is right, he usually is, but I wish to indulge in a counterargument even if it ultimately only proves his point.

He gives as his example of granular coding this:

    ClearAll[returnedQ,randomSteps,runExperiment,allReturns,stats];
    
    returnedQ[v_,steps_]:=MemberQ[Accumulate[v[[steps]]],{0,0}];
    
    randomSteps[probs_,q_]:=RandomChoice[probs->Range[Length[probs]],q];
    
    runExperiment[v_,probs_,q_]:= returnedQ[v,randomSteps[probs,q]];
    
    allReturns[n_,q_,v_,probs_]:= Total @ Boole @ Table[runExperiment[v,probs,q],{n}]
    
    stats[z_,n_,q_,v_,probs_]:=Table[allReturns[n,q,v,probs],{z}];

I have expressly left out the explanatory comments.  Answering questions on Stack Exchange has taught me that code often doesn't do what descriptions claim it does, and it is better to read and understand the code itself for a true understanding.

**I find the level of granularity illustrated above distracting rather than illuminating.**

- There is quite a lot of abstract fluff in the form of function names to tell me what code does rather that just *showing* me what it does in simple, reabable steps.

- Each subfunction has multiple parameters and the relationship between these functions is not clear at a glance.  The evaluation order ultimately proves simple but the code itself feels convoluted.

- To follow this code I have to read it backwards, working inside out, and I have to keep track of multiple arguments at each step.  Leonid wisely keeps the parameters consistent throughout but this *cannot* be assumed at first read, therefore additional mental effort must be expended.

Conversely in my own terse paradigm I would write the function as follows:

    ClearAll[stats2]

    stats2[z_, n_, q_, v_, probs_] :=
      With[{freq = probs -> Range @ Length @ probs},
        (
          v[[ freq ~RandomChoice~ q ]]
            // Accumulate
            // MemberQ[{0, 0}]
            // Boole
         ) ~Sum~ {n} ~Table~ {z}
      ];

**I find this greatly superior for personal ease of reading and comprehension.**

I know that my style is unconventional and at times controversial; some no doubt flinch at my use of ~infix~ operators.  Nevertheless I stand by my assertion that once this becomes familiar the code is very easy to read.

- The entire algorithm is visible in one compact structure
- The relationship of the parts of the code is quickly apparent
- The code can be read in a straightforward top-to-bottom, left-to-right manner
- This has almost no abstract fluff; the code is what it does, one comprehensible step at at time
- There is little need to visually or mentally jump around the code in the process of following it
- There are a minimum of arguments to keep track of at each step; each function is a built-in and each here has only one or two arguments, most instantly apparent from the syntax itself, e.g. `1 // f` or `1 ~f~ 2`.
- Each parameter (of `stats2`) is used only once, with the exception of `probs`; there is no interwoven handing off of arguments to track or debug (e.g. accidentally passing two in reverse order)
- There is virtually no need to count brackets or commas

I feel that as illustrated `stats2` is a sufficiently granular piece of code and that understanding and debugging it in its entirety is faster and easier than the same process on Leonid's code.

**So where are the questions in all of this?**

1. Who is right here? ;^) I know that my code is faster for *me* to read and understand, now and later.  But what do others make of it?  Surely some readers are already familiar with my style (perhaps grudgingly!) -- do they find `stats2` easy to read?

1. If as I believe there should be a balance of granularity and terseness how might the optimum degree be found?

1. Is my finding Leonid's code comparatively slow to read and follow peculiar?  What methods might I employ to improve my comprehension of that style?

1. If my code is *not* easy for others to read and follow how can I identify and address the barriers that make it so?

1. Am I missing the point?  Are ease and speed of reading and debugging not the primary goals of the coding style Leonid illustrated in this example?  What then is, and does my style fail to meet this goal in this specific example?

----------

### Reply 1

This is a reply specifically to Leonid, not because other answers are not equally welcome and valid but because I chose *his* statements and code as the basis for my argument.

I suspect that there is little in this that I truly disagree with and that further dialog will bring me closer to your position.  I have neither the breadth (multiple languages) nor depth (large projects, production code) of your experience.

I suspect that this is the crux of the problem: **"It is somewhat an art to decide for each particular case, and this can not be decided without a bigger context / picture in mind."**  I think that *art* is what I wish to explore here.

It is somewhat unfair to pick apart your example *without context* but since none was provided I see no other option.

I am certainly guilty of crafting "write-only code" at times; sometimes I even find this [amusing][1].  However I do not think `stats2` is a case of this.  To the contrary I find it more *read-friendly* than your code which is largely the foundation of this entire question.

I abhor code redundancy to the point of compulsively compacting other people's answers<sup>[(1)][2][(2)][3]</sup>, so your claim (if I read it correctly) that my style is inherently more redundant is simultaneously promising and exasperating. :^)

Surely I believe in code reusability, but I favor shorthand and abstractions that are *broadly applicable* rather than limited to a small class or number of problems.  What experienced coder doesn't have a shorthand for `Range @ Length @ x` because that comes up frequently in a broad range of problems?  But when I am going to use `returnedQ` again and is it worth the mental namespace to remember what it does?  Am I going to be looking for element `{0,0}` again or might it be something else?  Might I want `Differences` instead of `Accumulate`?  Is it easier to make `returnedQ` sufficiently general or to simply call `// MemberQ[foo]` when I need it?

You wrote:

> My guess is that you like terse code because it brings you to the solution most economically. But when / if you want to solve many similar problems most economically, then you will notice that, if you list all your solutions, and compare those, your terse code for all of them will contain repeated pieces which however are wired into particular solutions, and there won't be an easy way to avoid that redundancy unless you start making your code more granular.

Perhaps surprisingly this is actually rather backward from the way it seems to play out for me.  It is easy to churn out verbose code with little thought for brevity and clarity; that is *economic* of my time to *write*.  But spending the effort to write terse and clear code as I attempted to do with `stats2` returns economy *when reading and reusing that code* because I can quickly re-parse and understand this code holistically rather than getting lost in a tangle of abstractions as I do with your code example.  (Sorry, but that's how I feel in this case.)  I do not want to have to run code to understand what it does; I want to be able to simply read it in the language I am acquainted with (*Mathematica*).

If in the course of solving multiple related problems I realize that there is redundancy in my code I can still pull out those elements and refactor my code.  The simple, visibly apparent structure makes this easy.

I think the only way I shall be able to see this from your perspective is to work on a sufficiently large example where your principles become beneficial, and where our styles would initially diverge.  I wonder if we can find and use such an example without pointlessly spending time on something arbitrary.

----------

### Reply 2

Your updated answer reads:

> What I didn't realize was that often, when you go to even more granular code, dissecting pieces that you may initially consider inseparable, you suddenly see that your code has a hidden inner structure which can be expressed even more economically with those smaller blocks. This is what Sessions has repeatedly and profoundly demonstrated throughout his book, and it was an important lesson for me.

I welcome this epiphany!  To remove redundancy from my code and make it even more terse is something I have striven for for years.  I think this can only come through a direct example (or series of examples) as in the microcosm your granularity is verbose rather than condensing.  How large a code base would we need to have for this level of granularity to condense code rather than expand it?

C is so verbose that I doubt I would be able to fully appreciate and internalize examples from the referenced book.  Does a *Mathematica*-specific example come to mind?


[1]: https://mathematica.stackexchange.com/q/676/121
[2]: https://mathematica.stackexchange.com/a/8925/121
[3]: https://mathematica.stackexchange.com/a/73904/121