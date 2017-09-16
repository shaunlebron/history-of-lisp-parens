## Nokolisp Commands

| Navigation Command | Description                               |
|:-------------------|:------------------------------------------|
| `↕`                | move cursor to select an expression       |
| `4`                | navigate out to parent list (exit if top) |
| `6`                | navigate into list (edit inline if atom)  |
| `-`                | exit editor (back to repl)                |

| Modify Command | Description                          |
|:---------------|:-------------------------------------|
| `n`            | insert new line                      |
| `y`            | delete                               |
| `6`            | edit inline (or navigates into list) |
| `b`            | double this                          |
| `v`            | swap this and next                   |
| `q`            | wrap line in `(quote ...)`           |

| Paren Command | Description       | Example            |
|:--------------|:------------------|:-------------------|
| `a`           | add parens        | `a` => `(a)`       |
| `r`           | remove parens     | `(a)` => `a`       |
| `w`           | wrap with next    | `a b` => `(a b)`   |
| `c`           | conjoin with next | `(a) b` => `(a b)` |

| Display Command | Description         |
|:----------------|:--------------------|
| `p`             | toggle pretty-print |
| `f`             | refresh             |
