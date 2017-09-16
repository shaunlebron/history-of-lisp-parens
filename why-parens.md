# Why Parens?

_We look to "History of Lisp" by John McCarthy in 1979_

The motivations of "mathematical neatness":

> "As a programming language, LISP is characterized by the following ideas:... the representation of LISP programs as LISP data...the LISP function eval that serves both as a formal definition of the language and as an interpreter... Towards the end of the initial period, it became clear that this combination of ideas made an elegant mathematical system as well as a practical programming language.  Then mathematical neatness became a goal...  This was partly motivated by esthetic reasons and partly by the belief that it would be easier to devise techniques for proving programs correct if the semantics were compact and without exceptions."<br>

The motivations for a "list processing language":

> "... my own research in [AI]... involved representing information about the world by sentences... Representing sentences by list structure seemed appropriate... a list processing language also seemed appropriate..."<br>

Some notation was needed to READ and PRINT lists:

> "The original idea was to produce a compiler, but this was considered a major undertaking, and we needed some experimenting... Therefore, we started by hand-compiling various functions... to provide a LISP 'environment'.  These included programs to read and print list structure.  I can't now remember whether the decision to use parenthesized list notation as the external form of LISP data was made then..."<br>
> "The READ and PRINT programs induced a _de facto_ standard external notation for symbolic information, e.g. representing `x + 3y + z` by `(PLUS X (TIMES 3 Y) Z)`... Any other notation necessarily requires special programming, because standard mathematical notations treat different operators in syntactically different ways."<br>

The formal definition accidentally became an interpreter:

> "simplifications made LISP into a... formalism for doing recursive function theory..."<br>
> "Another way to show that LISP was neater than Turing machines was to write a universal LISP function and show that it is briefer and more comprehensible than the description of a universal Turing machine... Writing _eval_ required inventing a notation representing LISP functions as LISP data, and such a notation was devised for the purposes of the paper with no thought that it would be used to express LISP programs in practice... S.R. Russell noticed that _eval_ could serve as an interpreter for LISP, promptly hand coded it, and we now had a programming language with an interpreter."

Having an interpreter discouraged helpful notation changes:

> "The unexpected appearance of an interpreter tended to freeze the form of the language, and some of the decisions... later proved unfortunate.  These included the COND notation for conditional expressions which leads to an unnecessary depth of parentheses..."<br>

A more conventional notation was planned but never happened:

> "Another reason for the initial acceptance of awkwardness in the internal form of LISP is that we still expected to switch to writing programs as M-expressions.  The project of defining M-expressions precisely and compiling them or at least translating them into S-expressions was neither finalized nor explicitly abandoned.  It just receded into the indefinite future, and a new generation of programmers appeared who preferred internal notation to any FORTRAN-like or ALGOL-like notation that could be devised."<br>
> "As a programming language LISP had many limitations.  Some of the most evident in the early 1960s were... lack of a good system for input-output of symbolic expressions in conventional notations.  All... were planned to be fixed in LISP 2... The project proved more expensive than expected, the collaboration proved more difficult than expected, and so LISP 2 was dropped."<br>
