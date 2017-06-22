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
- 1987 - Interlisp SEdit (based on its previous DEdit and its unnamed teletype editor)
- ...
- [1980](https://news.ycombinator.com/item?id=10548242) - Zmacs by Scott Burson and David Chapman
- ...
- 1966 - [PILOT] (first thesis on structured editing)

### Researching methods

Researching old methods is difficult, but I've been tracing from this quote in
[Paredit credits], (but I could not locate `sedit.el`):

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

## Interlisp

> reimplemented by [LispEdit]

### Stored as data, not text

> In Interlisp, the programmer worked with source code presented by a structure
> editor, which operated on source code in the form of memory-resident Lisp data
> structures.

from [Evolution of Lisp]

### Teletype Editor

From the 1983 [Interlisp Reference Manual],
Chapter 17 describes "The Teletype Editor", a command-driven way to navigate and
modify S-expressions.  This is interesting because:

- only shows one expression at a time on a single line
  - (line-based editing as opposed to screen-based editing)
- nested sub-expressions collapsed by default to `&`
- expand with `?`
- pretty-print with `pp`

Since there is explicitly __one expression in focus at a time__, I believe this
allowed the following __paren inference__ via inserting a Right or Left paren:

> We could use a command which effectively inserts and/or removes left and right
> parentheses.
>
> There are six of these commands:
> - BI ("Both In"), BO ("Both Out")
> - LI ("Left In"), LO ("Left Out"
> - RI ("Right In"), RO ("Right Out")
>
> ...LI, LO, RI, and RO actually do not insert or remove just one parenthesis.
> but this is very suggestive of what actually happens.

An interesting way of describing parens:

> Of course, we will always have the same number of left parentheses as right
> parentheses, because the parentheses are just a notational guide to structure
> that is provided by our print program.

Touting "always balanced" here.

> Herein lies one of the principal advantages of a LISP oriented editor over a
> text editor: unbalanced parentheses errors are not possible.

### DEdit

Chapter 20.1 covers "DEdit", a more visual way to navigate and modify S-expressions
that still provides same commands from the teletype editor.

...

### SEdit

from the 1987 Xerox Lisp Release Notes:

> SEdit is the new Xerox Lisp structure editor. It allows you to edit
> Xerox Lisp code directly in memory.  This editor replaces DEdit in
> Chapter 16, Structure Editor, of the Interlisp-D Reference Manual.
> First introduced in Lyric, the SEdit structure editor has been greatly
> enhanced in the Medley release.

[![sedit-screen]][sedit-video]

- For full documentation, see Appendix B of [Lyric Release Notes] for initial
  version or [Medley Release Notes] for expanded version.
- extra resources for possibly running it:
  - https://www.reddit.com/r/lisp/comments/6iq2u8/how_was_lisp_edited_in_the_80s_and_90s/dj8n6yw/
- musings on SEdit
  - http://legacy.python.org/search/hypermail/python-1994q3/0136.html
  - http://legacy.python.org/search/hypermail/python-1994q3/0138.html

## LISP/VM

> I must say that I wish I could use LISP/VM again, and Martin's editor. I've
> always felt it gave me the best interface, with the highest productivity, of any
> editor I've ever used for LISP.
> (source: https://groups.google.com/d/msg/comp.lang.lisp/D2Q5t8IEOkg/EjgB3XBP8hQJ)

In the 1984 [LISP/VM User's Guide]

- misc note: https://groups.google.com/forum/#!topic/comp.lang.lisp/1q2qwkfFzKg

...

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

## Contemporary discussions on structured editing

- Prune: https://www.facebook.com/notes/kent-beck/prune-a-code-editor-that-is-not-a-text-editor/1012061842160013/
- Frame-based editing: https://news.ycombinator.com/item?id=14609215

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
[Interlisp Reference Manual]:http://www.softwarepreservation.org/projects/LISP/interlisp-d/3100186-Interlisp_Oct83.pdf
[History of Interlisp discussion]:https://groups.google.com/forum/#!topic/comp.sys.xerox/FKG8f1cnWvI

[sedit-screen]:https://user-images.githubusercontent.com/116838/27450864-b4ffcf20-5752-11e7-90e4-1668709d0189.png
[sedit-video]:https://www.youtube.com/watch?v=2qsmF8HHskg
[Lyric Release Notes]:http://bitsavers.trailing-edge.com/pdf/xerox/interlisp-d/198706_Lyric/198706_3102434_Lyric_Release_Notes.pdf
[Medley Release Notes]:http://bitsavers.trailing-edge.com/pdf/xerox/interlisp-d/198809_Medley_1.0/400006_Lisp_Release_Notes_Medley_Release_1.0_Sep88.pdf

[An Introduction to to Medley]:https://archive.org/details/bitsavers_xeroxinter0AnIntroductiontoMedleyRelease2.0Feb92_9578080
[Medley]:http://top2bottom.net/medley.html

[LISP/VM User's Guide]:http://www.softwarepreservation.org/projects/LISP/ibm/SH20-6477_LispVMUG_Jul84.pdf
