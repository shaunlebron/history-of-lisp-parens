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

In the 1983 [Interlisp Reference Manual], Chapter 17 describes "The Teletype Editor"
which is a command line way to navigate and modify S-expressions.  This is interesting
because it is

Chapter 20.1 covers "DEdit", a more visual way to navigate and modify S-expressions
that still provides same commands from the teletype editor.

Most interesting so far:

[Interlisp Reference Manual]:http://www.softwarepreservation.org/projects/LISP/interlisp-d/3100186-Interlisp_Oct83.pdf


> We could use a command which effectively inserts and/or removes left and right
> parentheses. There are six of these commands: 8 I ("Both In"), 80 ("Both Out"),
> LI ("Left In"), LO ("Left Out"), RI ("Right In"), and RO ("Right Out"). Of
> course, we will always have the same number of left parentheses as right
> parentheses. because the parentheses are just a notational guide to structure
> that is provided by our print program. Herein lies one of the principal
> advantages of a LISP oriented editor over a text editor: unbalanced parentheses
> errors are not possible. Thus. LI. LO, RI, and RO actually do not insert or
> remove just one parenthesis. but this is very suggestive of what actually
> happens.
