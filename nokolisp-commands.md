## Nokolisp Commands

| Paren Command | Description                    |
|:--------------|:-------------------------------|
| `a`           | wrap                           |
| `r`           | unwrap                         |
| `w`           | join with next line, then wrap |
| `c`           | extend parens to next line     |

| Display Command | Description         |
|:----------------|:--------------------|
| `p`             | toggle pretty-print |
| `f`             | refresh             |

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
