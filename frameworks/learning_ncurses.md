# Learning ncurses

## Formatting Text

The functions that control the tone of the text displayed on
the screen are, `attrset(attr)` sets the text attribute, `attron(attr), attroff(attr)` turns on or off specific attributes.

`attrset(attr)` turns off all the previous attributes, `attron(attr)` adds new attributes to the previous ones.

| Attribute    | What it does ?                                                                               |
| ------------ | -------------------------------------------------------------------------------------------- |
| A_ALTCHARSET | Displays text using an alternative character set (defined by your terminal)                  |
| A_BLINK      | Annoying blinking text                                                                       |
| A_BOLD       | Bright text, bold text, thick text (depending on terminal type)                              |
| A_DIM        | Dimmed text (not as bright as regular text)                                                  |
| A_INVIS      | "Hidden text" (available only on certain terminals)                                          |
| A_NORMAL     | Normal text                                                                                  |
| A_REVERSE    | Inverse text                                                                                 |
| A_STANDOUT   | Same as standout()                                                                           |
| A_UNDERLINE  | Underline text                                                                               |
| A_PROTECT    | "Protected text," available only on certain terminals, prevents text from being overwritten. |
| A_HORIZONTAL |                                                                                              |
| A_LEFT       |                                                                                              |
| A_LOW        |                                                                                              |
| A_RIGHT      |                                                                                              |
| A_TOP        |                                                                                              |
| A_VERTICAL   | Not implemented                                                                              |

### Colors in ncurses

`has_colors()` is used to check whether the terminal supports the color on not, it returns TRUE if the terminal is able to display colored text, FALSE otherwise, then `start_color()` is used to enable ncurses color abilities.

| NCURSES NUMBER | PC BIOS NUMBER | PC NAME | NCURSES NAME  |
| -------------- | -------------- | ------- | ------------- |
| 0              | 0              | Black   | COLOR_BLACK   |
| 1              | 4              | Red     | COLOR_RED     |
| 2              | 2              | Green   | COLOR_GREEN   |
| 3              | 6              | Brown   | COLOR_YELLOW  |
| 4              | 1              | Blue    | COLOR_BLUE    |
| 5              | 5              | Magenta | COLOR_MAGENTA |
| 6              | 3              | Cyan    | COLOR_CYAN    |
| 7              | 7              | White   | COLOR_WHITE   |

The `init_pair(pair, f, b)` is used to set the color pairs, example `init_pair(1, COLOR_YELLOW, COLOR_RED)` it is yellow text on a red background, to apply it use `attrset(COLOR_PAIR(1))`.

`init_color(color, r, g, b)` is used to create user defined colors, to check if terminal supports or not use `can_change_color()`.

`bkgd()` is used to set background color of terminal.

## Window, the terminal

### Getting the terminal size

`getmaxyx(win, y, x)` is used to get the size of the terminal, the `LINES` and `COLUMNS` constant also provide the size of the terminal but with respect to standard screen.

`getyx(win, y, x)` is used get the current position of the cursor.

## Moving curses around

`move(y, x)` is used to move the cursor, other functions are `mvaddch(y,x,ch)`, `mvaddstr(y,x,*str)`, `mvprintw(y,x,format,arg[...])`.

## Text manipulation

The `insch()` inserts a character, `insertln()` inserts a blank line of text, `delch()` deletes a single character or a line of text.

### Erase the screen

The `erase()` and `clear()` clears the screen, the `clrtobot()` function clears from the cursor’s current position to the bottom of the screen, And `clrtoeol()` clears from the cursor’s position to the end of the current line.

## Keyboard

Usually `getch()` blocks the program execution, but to prevent it use `nodelay(stdscr, TRUE)`, the `ungetch(ch)` function places the character ch back to the input buffer.
