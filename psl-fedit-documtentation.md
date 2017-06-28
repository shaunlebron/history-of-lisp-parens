# Portable Standard Lisp fedit documentation

*NOTE*: This was scanned and optical-character-recognitioned on 20170628 from pages 11 to 16 of the **Cambridge Lisp Reference Manual** published by Acorn Computers Ltd in 1985; ISBN 0 907876 42 0.

This edition refers to the National Semiconductor 32000 port of Acorn Cambridge Lisp, but the later ARM port had the same features. I do not know for certain that Portable Standard Lisp on other platforms had **fedit**/**sedit**, but I believe that they did because my understanding is that Cambridge Lisp was a fairly straight port of Portable Standard Lisp to the Acorn Cambridge Workstation (National Semiconductor 32016) and Archimedes (ARM) architectures. Similarly, as my understanding is that Portable Standard Lisp is just Standard Lisp with a Lisp-to-C compiler, I believe that **fedit**/**sedit** were inherited from Standard Lisp.


## 2.2 The LISP Editor

### 2.2.1 Introduction

The Cambridge LISP full-screen editor described in this document is a powerful structure editor written entirely in LISP. It may be invoked via two functions: the first of these, **sedit** , edits the s-expression given as its argument. The edited copy is returned. **fedit** edits the definition of a function given the function's name as an argument; the display portion of the editor has been especially tuned for editing function definitions. As well as edit existing functions, **fedit** can be used to create new ones. specifying the type of the function as an optional second argument. i.e.

    (fedit myfunction fexpr)

The editor sets up a template for the function, and the user fills in its definition using the normal editor commands. If **myfunction** already exists, the second argument is ignored, and the editor entered as normal. On exit from **fedit**, the edited function is compiled if the variable **\*comp** is currently set to a non-nil value. The function is also checked to see if it has been changed from an expr/lexpr to a fexpr (or vice-versa), and if so a warning message is printed that unexpected effects might occur on calls to the function from compiled code.

### 2.2.2 General background

The editor commands are designed around the concept of the 'current s-expression', which is visible on the screen at all times, the first character of which is highlighted by an inverse-video block (the 'edit pointer'). The current s-expression can be any one of the following:

1. an atom;
2. a LISP list starting with an opening parenthesis.
3. The cdr (tail) of a LISP list: in this case the inverse-video block is over the blank immediately before the car (head) of the current s-expression.

Initially, on entry to the editor, the current s-expression is the whole of the structure being edited, and the screen will resemble figure 1.

    h[ead] t[ail] u[p] b[egin] l[oo]k-f[or] ma[rk]-mo[ve] z[oom]i[n]-z[oom]o[ut]
    d[elete] r[eplace] s[plice] i[nsert] [u]n[do] c[hange] [e]x[plode] #[hash]
    e[val] w[indup] q[uit]    ?[redraw]

        (lambda (a b)
            (cond
                ((null a) b)
                (t
                    (cons
                        (car a)
                        (append & b) ) ) )

*Figure 1 The Lisp Editor The three lines at the top of the screen form a menu containing the more important (mostly single character) editor commands; then the structure being edited is displayed (in this case a function definition). The ampersands (&) indicate detail that has had to be suppressed for the structure to fit on the vdu screen.*

### 2.2.3 Editor commands

#### Elementary moving

When the arrow keys are pressed, the edit pointer does not move from character to character like a cursor in a text editor (e.g. the Panos editor), but jumps from one s-expression to the next. The best way to familiarise yourself with the edit pointer's style of movement is to experiment. In addition to using the arrow keys, there are several commands to move the edit pointer around, and thus make other parts of the structure the current s-expression. They are:

* h - Move to the head of the current s-expression.
* t - Move to its tail.
* u - Move up one level; inverse of head and tail.
* b - Move back up to the beginning of the smallest enclosing list.

#### Find and move

The next four commands perform more complicated location changing, the first two prompting at the bottom of the screen for an s-expression for the command to find.

* lf - Look for and move to the next occurrence (in print order) of the user-specified s-expression. The area in which the search takes place starts at the s-expression immediately after the current one, and the search begins at the end of the function, as it appears on the screen.
* lk - Look for and move to the next occurrence (in reverse print order) of the user-specified s-expression, the search beginning with the s-expression immediately before the current one.
* l - Repeat the last look for command.
* ma - Insert a mark at the current edit position. The mark is a new GENSYM ed atom of the form M00\<n\>.
* mo - Move to a previously set up mark.

#### Structure modification

The following commands perform structure modifying operations:

* d - Delete the current s-expression.
* r - Replace current s-expression with a user-specified s-expression read from the bottom of the screen. See also section 2.2.4 below headed `hash variables'.
* c - Repeat the last structure modification.
* i - Insert a user-specified s-expression at the edit pointer, performing a cons of the user's expression with the current s-expression.
* s - Splice in a user-specified list at the edit pointer. If the current s-expression is an atom, it is replaced by the elements in the new list.
* n - Undo the last structure modification command. A record is kept of all the modifications made to the structure, and successive undo commands will restore the funct to its state prior to editing.
* x - Explode the current s-expression so that it can be modified using one of the commands above.

#### Reformatting the screen

The next three commands change the appearance of the screen:

* ? - Reinitialise screen, and redisplay (useful if the screen has been messed up for some reason).
* zi - Zoom in and display current s-expression in more detail. The command will work only when the edit pointer is not at the top of the screen.
* zo - Zoom out; opposite of zoom in. The zoom is not allowed if it would cause the current s-expression itself to be supressed as a detail.

#### Eval loop and leaving the editor

The final three commands allow the user to enter a read-eval-print loop while still inside the editor, and allow the user to terminate the edit session and exit:

* e - Enter a read-eval-print loop; typing 'fin' terminates the loop and causes the editor to be reentered.
* w - Windup and update edited structure.
* q - Quit and do not update structure.

### 2.2.4 Entering an s-expression to the editor

The 'find', and some of the structure modification commands, require the user to enter an s-expression; in these cases the user is prompted at the bottom of the screen by ?. The s-expression input can cover as many lines as desired, the \[DELETE\] key deleting the last character typed (even back across previous lines), and \[TAB\] inserting three spaces. Typing \[ESCAPE\] at any point completely abandons the current command.

#### Hash Variables

For convenience, in 'cut and paste' operations, the editor sets up the variable #0 to contain the current s-expression, and, if it is a list, #1, #2,... to contain the values of the top-level elements of it. There is also the command '#' which sets the value of the variable # to be the current s-expression at the time the command was issued. The values of these #- variables are substituted into each s-expression and typed wherever they occur in it. These #-variables are also available in the read-eval-print loop inside the editor invoked by the eval command.

#### Miscellaneous features

The editor stores the name of the last function it edited in the global variable **\*\*edit-last-function**, and if the function editor is called without being given the name of a function, it re-edits the last one.

The menu of editor commands displayed at the top of the screen can be changed by altering the contents of the global variable **\*\*edit-menu**. The variable must contain a list of strings, each not longer than the width of the screen, each string to go on one line. The position on the screen of the structure being edited is automatically adjusted depending on how much space the menu takes up.

Since there is the facility to enter a supervisor loop within the editor, it is possible (and sometimes very useful) to enter the editor within that loop and thus edit at a second (or even higher) level. To help the user keep track of which level he is in, and the name of the function he is editing at each level, the editor maintains this information in the variable **\*\*edit-Level**.

The editor maintains a list of all the functions that have been edited in the current LISP session in the global variable **\*\*edit-functions**. Thus it is easy to keep track of which functions have been changed and so need to he written hack out to disc at the end of a session.

#### 2.2.5 limitations

The editor cannot deal with reentrant LISP s-expressions. Currently it cannot express vectors or strings adequately for easy editing of their internal constituents.
I
1





