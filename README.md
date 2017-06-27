# History of Lisp Editing

I'd like to find out how people tolerated parens back in the golden days of
Lisp. I have a feeling we might've forgotten some things that would be useful
today, or might influence some new ideas.

I started by working backwards from today (still filling in blanks):

- 2015 - [Parinfer]
- 2014 - [Lispy]
- 2012 - [Smartparens]
- 2005 - [Paredit] by [Taylor Campbell]
- 2001 - [DrScheme], now [DrRacket]
- ...
- 1987 - Interlisp SEdit (structure editor. full interactive display)
- 198? - Interlisp DEdit (display editor. clickable display + command window)
- 1980 - IBM Lisp/VM Lispedit (display editor)
- 1980 - Zmacs - first structure commands for text editor
- ...
- 1967 - BBN (InterLisp) - (teletype structure editor.)
- 1966 - [PILOT] - first thesis on structure editing

## Interlisp

> In Interlisp, the programmer worked with source code presented by a structure
> editor, which operated on source code in the form of memory-resident Lisp data
> structures.<br>—[Evolution of Lisp]


### Teletype Editor

__[Try it here!](running.md#interlisp-teletype)__

A command-line interface for editing s-expressions. Rather than displaying the
whole file, only one expression is displayed at a time—by printing after each
command.

- use `N` to go Nth child of current expression
- use `0` to go up to parent
- nested sub-expressions collapsed by default to `&`
- expand with `?`
- pretty-print with `pp`

Six paren commands can be performed on the current expression's children:

| Command | Name      | Mnemonic | Extra Inference                     |
|:--------|:----------|:---------|:------------------------------------|
| `BI`    | Both In   | `()+`    |                                     |
| `BO`    | Both Out  | `()-`    |                                     |
| `LI`    | Left In   | `(+`     | adds `)` at end                     |
| `LO`    | Left Out  | `(-`     | removes `)` and EVERYTHING AFTER IT |
| `RI`    | Right In  | `)<`     |                                     |
| `RO`    | Right Out | `)>`     |                                     |

```
(A B C D E F G H)

>(BI 3)
(A B (C) D E F G H)
     ^ ^ wrap parens around index 3
```

```
(A B C D E F G H)

>(BI 3 5)
(A B (C D E) F G H)
     ^     ^ wrap parens from index 3 to index 5

>(BO 3)
(A B _C D E_ F G H)
     ^     ^ unwrap parens around index 3
```

```
(A B C D E F G H)

>(LI 3)
(A B (C D E F G H))
     ^           ^ insert left-paren before index 3, and right-paren at end
```

```
(A B (C D E) F G H)

>(LO 3)
(A B _C D E_ _ _ _)
     ^     ^ ^ ^ ^ remove parens around index 3, and EVERYTHING AFTER IT
```

```
(A B (C D E F G H))

>(RI 3 2)
(A B (C D) E F G H_)
         ^ <----- ^ move right-paren of index 3 to inner index 2

>(RO 3)
(A B (C D_ E F G H))
         ^ -----> ^ move right-paren of index 3 to end
```

_See the 1967 [BBN Lisp System] section on "structure changing commands" page 49._


### DEdit

The display editor was a visual alternative to the teletype editor—click one or
two expressions in the pretty-print, then click a command to execute on those
expressions.

1. __pretty-print window__ (left) - click to select expressions (current=solid-lined, previous=dash-lined)
1. __command menu__ (right) - click to perform an operation on selections (current=arg1, previous=arg2)
1. __type-in window__ (below) - manually type an expression. when done, it becomes selected and clickable

![dedit-screen]

Clicking an expression while holding <kbd>Shift</kbd>
_unreads_ it into the type-in window (pastes as text).

- __left click__ - select object
- __middle click__ - select containing list
- __right click__ - select lowest common ancestor with previous selection

| DEdit Paren Command | Initially Hidden?             | Teletype Command |
|:--------------------|:------------------------------|:-----------------|
| `()`                |                               | same as `BI`     |
| `( in`              | middle-click `()` to show     | same as `LI`     |
| `) in`              | middle-click `()` to show     | same as `RI`     |
| `() out`            |                               | same as `BO`     |
| `( out`             | middle-click `() out` to show | same as `LO`     |
| `) out`             | middle-click `() out` to show | same as `RO`     |

_See the 1985 [Interlisp-D Reference Manual Volume II: Environment], Chapter 16
page 407._

### SEdit

__[Try it here!](running.md#interlisp-sedit)__

from the 1987 Xerox Lisp [Medley Release Notes]:

> SEdit is the new Xerox Lisp structure editor. It allows you to edit
> Xerox Lisp code directly in memory.  This editor replaces DEdit in
> Chapter 16, Structure Editor, of the Interlisp-D Reference Manual.
> First introduced in Lyric, the SEdit structure editor has been greatly
> enhanced in the Medley release.

[![sedit-screen]][sedit-video]

See [SEdit Caret and Selection details] to learn how to edit. Parentheses
behavior below:

[SEdit Caret and Selection details]:sedit-caret-selection.md

| Paren Operation  | Description                                                     |
|:-----------------|:----------------------------------------------------------------|
| Type `(`         | inserts `()` with `▲` inside                                    |
| Type `)`         | nothing inserted. places `▲` after next `)`. selects whole list |
| Backspace at `(` | removes list if empty, else no-op                               |
| Backspace at `)` | nothing deleted. places `▲` before `)`                          |
| Middle-click `(` | selects list. places `▲` on clicked side of `(`                 |
| Middle-click `)` | selects list. places `▲` on clicked side of `)`                 |
| Meta-`(`         | wraps selection in a list. places `▲` after `(`                 |
| Meta-`)`         | wraps selection in a list. places `▲` after `)`                 |
| Meta-`/`         | unwraps selected list, string, or quote                         |

_See Appendix B of [Lyric Release Notes] or [Medley Release Notes]_

musings on SEdit
  - http://legacy.python.org/search/hypermail/python-1994q3/0136.html
  - http://legacy.python.org/search/hypermail/python-1994q3/0138.html

## ZMacs

ZMacs in 1980 is [reported](https://news.ycombinator.com/item?id=10548242) to be
the first text editor with balanced parentheses commands. The 1987 [ZMacs
Editor Reference] shows them on page 209 (3-137):


## Lispedit

> I must say that I wish I could use LISP/VM again, and Martin's editor. I've
> always felt it gave me the best interface, with the highest productivity, of any
> editor I've ever used for LISP.
> —[Cyril N. Alberga](https://groups.google.com/d/msg/comp.lang.lisp/D2Q5t8IEOkg/EjgB3XBP8hQJ)

> An important feature of Lispedit is a program display that shows the structure
> of a Lisp expression from the point of view of a selected sub-expression.  The
> sub-expression, called the _focus_, is shown high-lighted and its relationship
> to the surrounding context is shown by automatically generated indentation.
> Selected components of the focus and its context are elided (shown as '...') in
> order to condense large expressions to the confines of a finite screen.
> —[Interactive program execution in Lispedit]

There are no surviving images of what Lispedit looked like.  But reconstructing
from descriptions:

<pre>
┌────────────────────────────────────────────────────────────────┐
│TOP DISPLAY AREA: pretty-printed and condensed code             │
│                  ("focus" expression highlighted)              │
│                                                                │
│  1  (LAMBDA                                                    │
│  2    (INPUT)                                                  │
│  3    (PROG (WORDLIST)                                         │
│  4      (DO ((I 0 (+ (FINDENDWORD INPUT I) 1))) ...)           │
│  5      (SETQ WORDLIST (REVERSE WORDLIST))                     │
│  6      <strong>(NMAPCAR                                               </strong>│
│  7      <strong>  (LAMBDA                                              </strong>│
│  8      <strong>    (WORD)                                             </strong>│
│  9      <strong>    (COND                                              </strong>│
│ 10      <strong>      (((ONE-OF a e i o u) (ELT WORD 0)) &)            </strong>│
│ 11      <strong>      ('ELSE                                           </strong>│
│ 12      <strong>        (CONCAT                                        </strong>│
│ 13      <strong>          (SUBSTRING WORD 1 (- (SIZE WORD) 1))         </strong>│
│ 14      <strong>          (SUBSTRING WORD 0 1)                         </strong>│
│ 15      <strong>          "ay "))))                                    </strong>│
│ 16      <strong>  WORDLIST)</strong> ...)                                       │
│                                                                │
├────────────────────────────────────────────────────────────────┤
│FENCE LINE: (recursion-level / input-state / current-object)    │
├────────────────────────────────────────────────────────────────┤
│MESSAGE AREA: (command messages echoed here)                    │
├────────────────────────────────────────────────────────────────┤
│Program Function Keys: (currently defined keys)                 │
├────────────────────────────────────────────────────────────────┤
│Command Area: _                                                 │
└────────────────────────────────────────────────────────────────┘
</pre>

_See the 1984 [LISP/VM User's Guide] and [Experience with an Uncommon Lisp]._

## Maclisp

(preferred formatted ASCII files over data structures for programs)

## Debating Maclisp vs Interlisp (i.e. storing code as text vs structure)

A discussion/debate from 1978 that reveals a lot about how people thought about
text vs structure when storing and displaying their code:

[Programming in an Interactive Environment: the Lisp Experience](https://www.researchgate.net/publication/220566511_Programming_in_an_Interactive_Environment_the_LISP_Experience)

- response by Richard Stallman arguing for text: https://www.deepdyve.com/lp/association-for-computing-machinery/surveyor-s-forum-structured-editing-with-a-lisp-PzoXAz9GCu?impressionId=594bfe8baf9dc&i_medium=mydeepdyve&i_campaign=recommendations&i_source=recommendations
- author's reply: https://www.deepdyve.com/lp/association-for-computing-machinery/surveyor-s-forum-structured-editing-with-a-lisp-mQNqMU2je0?impressionId=594c0f05171ea&i_medium=docview&i_campaign=recommendations&i_source=recommendations
- a much later followup discussing how structured editing died: https://groups.google.com/forum/#!msg/comp.lang.lisp/D2Q5t8IEOkg/AqbNfOxZgUIJ
  - Maclisp killed it because they wanted custom layout of code and comments

This is so far my favorite summary of this topic from 1997.  (too many great
points to list).
https://groups.google.com/d/msg/comp.lang.lisp/dldLx8Yj7q8/u4y2zq19XIYJ

## Appendix

### Non-Lisp discussions on structure editing

- Prune: https://www.facebook.com/notes/kent-beck/prune-a-code-editor-that-is-not-a-text-editor/1012061842160013/
- Frame-based editing: https://news.ycombinator.com/item?id=14609215
- Intentional Programming: https://www.youtube.com/watch?v=tSnnfUj1XCQ
  - similar to Interlisp (i.e. structure-based)

### Researching methods

started from [Paredit credits], (could not locate `sedit.el`):

> The original inspirations for paredit were Interlisp-D's structure
> editor 'SEdit' -- a real structure editor, not a cheesy imitation like
> paredit -- and Guillaume Germain's sedit.el for GNU Emacs.

- finding mailing list discussions
- looking for official reference manuals of lisp machines
- using [deepdyve] to find articles
- asking around

General:
  - [Evolution of Lisp] seems to provide a good map.
  - http://www.softwarepreservation.org/projects/LISP/


[Parinfer]:http://shaunlebron.github.io/parinfer/
[Lispy]:https://github.com/abo-abo/lispy
[Smartparens]:https://github.com/Fuco1/smartparens
[Paredit]:https://www.emacswiki.org/emacs/ParEdit
[Paredit credits]:http://mumble.net/~campbell/emacs/paredit.credits
[DrScheme]:http://www.ccs.neu.edu/racket/pubs/jfp01-fcffksf.pdf
[DrRacket]:https://docs.racket-lang.org/drracket/editor.html
[Taylor Campbell]:http://mumble.net/~campbell/
[PILOT]:https://dspace.mit.edu/bitstream/handle/1721.1/6905/AITR-221.pdf

[LispEdit]:https://github.com/blakemcbride/LispEdit/blob/master/EDIT.txt
[deepdyve]:https://www.deepdyve.com
[Evolution of Lisp]:https://www.csee.umbc.edu//courses/331/resources/papers/Evolution-of-Lisp.pdf
[BBN Lisp System]:http://www.dtic.mil/dtic/tr/fulltext/u2/656771.pdf
[Interlisp Reference Manual]:http://www.softwarepreservation.org/projects/LISP/interlisp-d/3100186-Interlisp_Oct83.pdf
[History of Interlisp discussion]:https://groups.google.com/forum/#!topic/comp.sys.xerox/FKG8f1cnWvI
[Interlisp-D Reference Manual Volume II: Environment]:http://www.mirrorservice.org/sites/www.bitsavers.org/pdf/xerox/interlisp-d/198510_Koto/3101273_Interlisp-D_Vol_2_Environment_Oct85.pdf

[dedit-screen]:https://user-images.githubusercontent.com/116838/27507672-6a6416ae-5899-11e7-9475-5704bb8933c4.png
[sedit-screen]:https://user-images.githubusercontent.com/116838/27450864-b4ffcf20-5752-11e7-90e4-1668709d0189.png
[sedit-video]:https://www.youtube.com/watch?v=2qsmF8HHskg
[Lyric Release Notes]:http://bitsavers.trailing-edge.com/pdf/xerox/interlisp-d/198706_Lyric/198706_3102434_Lyric_Release_Notes.pdf
[Medley Release Notes]:http://bitsavers.trailing-edge.com/pdf/xerox/interlisp-d/198809_Medley_1.0/400006_Lisp_Release_Notes_Medley_Release_1.0_Sep88.pdf

[An Introduction to to Medley]:https://archive.org/details/bitsavers_xeroxinter0AnIntroductiontoMedleyRelease2.0Feb92_9578080
[Medley]:http://top2bottom.net/medley.html

[LISP/VM User's Guide]:http://www.softwarepreservation.org/projects/LISP/ibm/SH20-6477_LispVMUG_Jul84.pdf
[ZMacs Editor Reference]:http://bitsavers.trailing-edge.com/pdf/ti/explorer/2243192-0001A_Zmacs_Jun87.pdf

[Experience with an Uncommon Lisp]:https://pdfs.semanticscholar.org/d15c/2d1a8d4b0086af487372504f50cbe9dbcae7.pdf
[Interactive program execution in Lispedit]:https://www.deepdyve.com/lp/association-for-computing-machinery/interactive-program-execution-in-lispedit-oIXwkiLVjG
