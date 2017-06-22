# History of Lisp Editing

I'd like to find out how people tolerated parens back in the golden days of
Lisp. I have a feeling we might've forgotten some things that would be useful
today, or might influence some new ideas.

I started by working backwards from today:

- 2015 - [Parinfer]
- 2014 - [Lispy]
- 2012 - [Smartparens]
- 2005 - [Paredit] by [Taylor Campbell]
- ...?

[Parinfer]:http://shaunlebron.github.io/parinfer/
[Lispy]:https://github.com/abo-abo/lispy
[Smartparens]:https://github.com/Fuco1/smartparens
[Paredit]:https://www.emacswiki.org/emacs/ParEdit
[Taylor Campbell]:http://mumble.net/~campbell/

Going back further is more difficult, but I found this quote in [Paredit
credits]:

> The original inspirations for paredit were Interlisp-D's structure
> editor 'SEdit' -- a real structure editor, not a cheesy imitation like
> paredit -- and Guillaume Germain's sedit.el for GNU Emacs.

[Paredit credits]:http://mumble.net/~campbell/emacs/paredit.credits

I could not locate `sedit.el`, but I started reading about Interlisp to find out
more.

## Interlisp

From the 1983 [Interlisp Reference Manual]

[Interlisp Reference Manual]:http://www.softwarepreservation.org/projects/LISP/interlisp-d/3100186-Interlisp_Oct83.pdf

### Teletype Editor

Chapter 17 describes "The Teletype Editor", a command-driven way to navigate and
modify S-expressions.  This is interesting because:

- only shows one expression at a time on a single line
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

SEdit is hailed as a great Lisp editor, but I can find no documentation for it.
The latest Interlisp manual I can find is from 1985, and it made no mention of
it, so it probably came out sometime after.

- Thoughts on SEdit
  - http://legacy.python.org/search/hypermail/python-1994q3/0136.html
  - http://legacy.python.org/search/hypermail/python-1994q3/0138.html

## LISP/VM

> I must say that I wish I could use LISP/VM again, and Martin's editor. I've
> always felt it gave me the best interface, with the highest productivity, of any
> editor I've ever used for LISP.
> (source: https://groups.google.com/d/msg/comp.lang.lisp/D2Q5t8IEOkg/EjgB3XBP8hQJ)

In the 1984 [LISP/VM User's Guide]

[LISP/VM User's Guide]:http://www.softwarepreservation.org/projects/LISP/ibm/SH20-6477_LispVMUG_Jul84.pdf

...


## Maclisp

...

## Misc Notes

- Prune: https://www.facebook.com/notes/kent-beck/prune-a-code-editor-that-is-not-a-text-editor/1012061842160013/
- Why Interlisp's structure editor disappeared: https://groups.google.com/forum/#!msg/comp.lang.lisp/D2Q5t8IEOkg/AqbNfOxZgUIJ
  - Maclisp killed it because they wanted custom layout of code and comments?
- Different Lisp systems: http://www.softwarepreservation.org/projects/LISP/
