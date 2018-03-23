# History of alternative syntaxes for Lisp

Lisp uses s-expressions. There is a long history of others that have been tried.

* 1958 - [M-expressions], Lisp's original intended syntax (never implemented)
* 1964 - [A-Language], algol syntax for LISP
* 1964 - [LISP 2], algol syntax (proposal)
* 1967 - [Logo], educational lisp (no outer parens, square brackets for inner nesting)
* 1967 - [Interlisp], added optional "Super Parentheses" for replacing `)))))...` with `]`
* 1968 - [MLISP], algol syntax for LISP 1.5
* 1970 - [RLISP], algol syntax for Standard LISP
* 1973 - [CLISP], Conversational LISP (s-expressions + infix/algol)
* 1977 - [CGOL], algol syntax for MACLISP
* 1992 - [Dylan], lisp derivative with algol syntax
* 1996 - [IACL2], infix support for ACL2, a Common Lisp variant
* 1997 - [Pico], an educational Scheme with easier syntax
* 2003 - [I-expressions], indentation-based
* 2006 - [PLOT], macro-compatible algol-like
* 2006 - [TwinLisp], C-like syntax for Common Lisp
* 2006 - [Readable], proposing three superset (c,n,t)-expressions
* 2008 - [Genyris], indentation-based
* 2009 - [Ginger], proposing g-expressions for "python aesthetics" ([backup link][ginger-backup])
* 2012 - [Honu], similar to PLOT, macro-compatible ([backup link][honu-backup])
* 2014 - [Wisp], a simplified version of "readable"
* 2015 - [Nonelang], with [naked expressions]

## Why move away from s-expressions?

> "Although LISP is one of the most powerful tools available ... the format of the input language (S-expression) is awkward to use -- so awkward that many errors in programming LISP stem directly from the fact that S-expressions are the only allowable form of input. The inherent difficulty of producing correctly working S-expressions is tacitly recognized by anyone who uses M-expressions in place of them, when not communicating directly with the computer."
> "... This simple function has 26 parentheses, and a long complicated program would have many more. This proliferation of parentheses makes it very difficult to write such complicated programs without an error in placement or pairing of parentheses."
> "Another inconvenience is the fact that Polish notation is mandatory... All this points toward the need for a more natural input language."<br> > **—An Auxiliary Language for More Natural Expression—the A-Language (1964)**

> "The syntax of [Lisp] is very simple, in the sense that it can be described concisely, but not in the sense that Lisp programs are easy to read or write! This simplicity of syntax is achieved by, and at the expense of, extensive use of explicit structuring, namely, grouping through parenthesization."
> "... most high level programming languages offer syntactic devices for reducing apparent depth and complexity of a program: the reserved words and infix operators used in Algol-like languages simultaneously delimit operands and operations, and also convey meaning to the programmer. They are far more intuitive than parentheses. In fact, since Lisp uses parentheses (i.e., lists) for almost all syntactic forms, there is very little information contained in the parentheses for the person reading a Lisp program, and so the parentheses tend mostly to be ignored: the meaning of a particular Lisp expression for people is found almost entirely in the _words_, not in the structure."<br> > **—Conversational Lisp (1973)**

## A-Language (1964)

A-Language allowed function calls delimited by custom word positions rather than parens. An example definition:

```
(DEFINE
  SUBSTITUTING                              ; name
  (THE RESULT OF FOR IN)                    ; auxiliary words to discard
  (7)                                       ; precedence level
  (THE RESULT OF SUBSTITUTING X FOR Y IN Z) ; example that locates the args relative to the name and auxiliary words to be discarded
  (SUBST X Y Z))                            ; body definition
```

An example usage of the above definition:

```
(IF
  THE RESULT OF SUBSTITUTING X FOR Y IN Z ; <- calls above definition
  EQUALS Z
  THEN PRINT Z ELSE X)
```

## Conversational Lisp (1973)

> Just as communication is based on the intention of the speaker to produce an effect in the recipient, Clisp operates under the assumption that what the user said was _intended_ to represent a meaningful operation, and therefore tries very hard to make sense of it.

Clisp embraces the natural ambiguity of human communication as a virtue. It is
simply a system that receives errors from the normal interpreter and tries to
resolve them depending on the types of values attached to names. Specifically,
it claims to be able to take errors resulting from infix notation and
algol-style function calls and translate them appropriately.

## RLISP

_See [The Portable Standard LISP Users Manual], Chapter 3_

[the portable standard lisp users manual]: http://www.softwarepreservation.org/projects/LISP/utah/USCP-Portable_Standard_LISP_Users_Manual-TR_10-1982.pdf

## Sources

* [Readable s-expressions and sweet-expressions...(2006)](https://www.dwheeler.com/readable/readable-s-expressions.html)
  * later expanded into a [large wiki resources and history](https://sourceforge.net/p/readable/wiki/Home/)
* [Top Down Operator Precedence (2007)](http://javascript.crockford.com/tdop/tdop.html)
* [The Evolution of Lisp (1993)](https://www.dreamsongs.com/Files/HOPL2-Uncut.pdf)
* [LISP Infix Syntax Survey (2013)](http://xahlee.info/comp/lisp_sans_sexp.html)
* [lispin.org similar links](http://web.archive.org/web/20070827030525/http://www.lispin.org:80/wiki?page=default/links)

## Appendix

### _Adding_ s-expressions to a language

* 2008 - [Lisp Flavored Erlang]
* 2013 - [Hylang]

### Mathematica

I can't tell how close Mathematica (Wolfram Language) is to Lisp. Some
evaluation differences, and `f[...]` for function calls, `{...}` for lists,
and `(...)` for grouping.

* [Mathematica v1 manual - 4.2.7 LISP](http://reference.wolfram.com/legacy/v1/contents/4.2.7.pdf)
* [There Was a Time before Mathematica](http://blog.stephenwolfram.com/2013/06/there-was-a-time-before-mathematica/)

[a-language]: http://www.softwarepreservation.org/projects/LISP/book/III_LispBook_Apr66.pdf#page=249
[cgol]: http://web.archive.org/web/20080218053546/http://zane.brouhaha.com/~healyzh/doc/cgol.doc.txt
[lisp 2]: https://en.wikipedia.org/wiki/LISP_2
[mlisp]: http://i.stanford.edu/pub/cstr/reports/cs/tr/68/92/CS-TR-68-92.pdf
[dylan]: https://en.wikipedia.org/wiki/Dylan_(programming_language)
[clisp]: http://www.softwarepreservation.org/projects/LISP/interlisp/Teitelman-3IJCAI.pdf
[m-expressions]: https://en.wikipedia.org/wiki/M-expression
[rlisp]: https://en.wikipedia.org/wiki/Reduce_(computer_algebra_system)
[readable]: https://sourceforge.net/p/readable/wiki/Home/
[logo]: http://el.media.mit.edu/logo-foundation/what_is_logo/logo_programming.html
[wisp]: https://srfi.schemers.org/srfi-119/srfi-119.html
[ginger]: http://sci-hub.tw/10.1145/1566445.1566481
[ginger-backup]: papers/palmer2009.pdf
[nonelang]: https://bitbucket.org/duangle/nonelang/overview
[naked expressions]: http://nonelang.readthedocs.io/en/latest/dataformat.html#naked-coated-expressions
[lisp flavored erlang]: https://en.wikipedia.org/wiki/LFE_(programming_language)
[hylang]: https://en.wikipedia.org/wiki/Hy
[interlisp]: http://www.dtic.mil/dtic/tr/fulltext/u2/656771.pdf
[plot]: http://users.rcn.com/david-moon/PLOT/
[i-expressions]: https://srfi.schemers.org/srfi-49/srfi-49.html
[honu]: http://sci-hub.tw/10.1145/2371401.2371420
[honu-backup]: papers/rafkind2012.pdf
[genyris]: http://lambda-the-ultimate.org/node/2651
[pico]: https://en.wikipedia.org/wiki/Pico_(programming_language)
[twinlisp]: http://twinlisp.nongnu.org/docs/TwinLisp%20for%20lisp%20users.html
[iacl2]: http://www.cs.utexas.edu/users/moore/infix/printer/syntax.html
