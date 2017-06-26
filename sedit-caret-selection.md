# SEdit Caret and Selection details

Two types of carets (cursors):

| Type            | Symbol              | Description                                 | Set with                             |
|:----------------|:--------------------|:--------------------------------------------|:-------------------------------------|
| Edit Caret      | `⌃`                 | caret is _inside_ an atom                   | left-click                           |
| Structure Caret | `▲`                 | caret is _between_ atoms                    | middle-click, or double left-click   |
| I-beam          | <code>&#124;</code> | pre-caret position before click is released | only shown when clicking or dragging |

Three types of selections:

| Type               | Style              | Description                              | Set with                     |
|:-------------------|:-------------------|:-----------------------------------------|:-----------------------------|
| Caret Selection    | underline          | moves in conjunction with the caret      | left-click or middle-click   |
| Extended Selection | box                | replaces caret and extends its selection | right-click                  |
| Copy Selection     | squiggly-underline | a parallel selection for copying text    | <kbd>Shift</kbd> + any-click |

## Edit Caret `⌃`

Left-clicking an atom selects an individual character, and places `⌃` to its
left or right:

```
(LEQ n 1)     ; left-click "Q" on its right side
   ─⌃

(LEQ n 1)     ; left-click "Q" on its left side
  ⌃─
```

When `⌃` is present, typing will insert text inside the atom.

```
(LEQ n 1)     ; 1. left-click "Q" on its right side
   ─⌃

(LEQX n 1)    ; 2. type "X"
     ⌃
```

Removing an atom or inserting a space will change to a structure caret `▲`.

## Structure Caret `▲`

Middle-clicking an atom selects it, and places `▲` to its left or right:

```
(LEQ n 1)     ; middle-click "Q" on its right side
 ───▲

(LEQ n 1)     ; middle-click "Q" on its left side
▲───
```

When `▲` is present, typing creates a new atom, and changes caret to `⌃`:

```
(LEQ n 1)     ; 1. middle-click "Q" on its right side
 ───▲

(LEQ X n 1)   ; 2. type "X"
      ⌃
```

Double middle-clicking an atom selects its containing list, and places `▲` to its right:

```
(LEQ n 1)     ; double middle-click "Q"
─────────▲
```

## Selections

Normal selections are shown underlined, and are made by clicking as shown previously.

Right-clicking creates "extended" selections indicated by boxes.

Subsequent typing replaces selection:

```
(LEQ n 1)     ; 1. left-click "E"
  ─⌃
  ┌──┐
(L│EQ│ n 1)   ; 2. right-click "Q"
  └──┘

(LX n 1)      ; 3. type "X"
   ⌃
```

```
(LEQ n 1)     ; 1. middle-click "E"
 ───▲
 ┌─────┐
(│LEQ n│ 1)   ; 2. right-click "n"
 └─────┘

(X 1)         ; 3. type "X"
  ⌃
```

## Selection Pasting

Holding <kbd>Shift</kbd> allows you to click around to create a parallel "copy"
selection, indicated with a squiggly underline. Caret and original selection are
not modified during this time.

Releasing <kbd>Shift</kbd> will paste the "copy" selection at the caret. If an
"extended" (boxed) selection is present instead of a caret, it is replaced by
the "copy" selection.

### Selection Commands

Selected text can also be modified by commands (for a menu, hold middle-click on "SEdit" in titlebar):

| Hotkey   | Name         | Description                                        |
|:---------|:-------------|:---------------------------------------------------|
| Meta-`J` | Join         | joins selected items together. places `▲` after it |
| Meta-`'` | Quote        | quotes selected items                              |
| Meta-`(` | Parenthesize | wraps selection in a list. places `▲` after `(`    |
| Meta-`)` | Parenthesize | wraps selection in a list. places `▲` after `)`    |
| Meta-`/` | Extract      | unwraps selected list, string, or quote            |

Custom mutation functions with Meta-`Z`.
