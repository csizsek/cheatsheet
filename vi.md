# vi Cheatsheet

## Command Line
| Command | Effect |
| --- | --- |
| $vi -r *file* | recover *file* and recent edits after a crash |
| $vi +*n* *file* | open *file* at line *n* |
| $vi -c *cmd* *file* | open *file* and execute *cmd* |

## Navigation Commands
| Command | Effect |
| --- | --- |
| w,W,b,B | forward, backward by word |
| },{ | beginning of next, previous paragraph |
| 0,$ | beginning, end of current line |
| ENTER | first non-blank character of next line |
| H,M,L | top, middle, last line of screen |
| CTRL-F CTRL-B | scroll forward, backward one screen |
| CTRL-D CTRL-U | scroll forward, backward one half-screen |
| CTRL-E CTRL-Y | scroll forward, backward one line |
| z . | reposition line to middle of screen |
| CTRL-G | display current line |
| *n* G | move to line *n* |
| G | move to last line |
| /,?*pattern* | search forward, backward for *pattern* |
| n,N | repeat search in same, opposite direction |
| /,? | repeat search forward, backward |

## Edit Commands
| Command | Effect |
| --- | --- |
| i,a | insert text before, after cursor |
| o,O | open new line for text below, above cursor |
| cw | change word |
| cc | change line |
| R | overwrite characters |
| x,X | delete character before, after cursor |
| dw,dd | delete current word, line |
| d *motion* | delete text between cursor and the target of *motion* |
| D | delete to the end of line |
| p,P | put text after, before current line |
| yw,yy | yank current word, line |
| y *motion* | yank text between cursor and the target of *motion* |
| u | undo last edit |
| U | restore current line |
| J | join two lines |

## Exit Commands
| Command | Effect |
| --- | --- |
| :w,:w! | save file, save file overriding protection |
| :wq,ZZ | save file and quit |
| :q,:q! | quit, quit overriding protection |
| :e! | return to version of current file as of time of last write (save) |

## Substitution and RegEx Commands
| Command | Effect |
| --- | --- |
| :[addr1[,addr2]]s/old/new/[flags] | the general form of substitution commands |
| c | confirm each substitution (goes to end) |
| g | substitute all occurrences on current line (goes to end) |
| % | substitute in the whole file (goes to beginning) |

| Wildcard | Effect |
| --- | --- |
| . | any single character except a newline |
| * | the previous character zero or more times |
| ^ | beginning of line |
| $ | end of line |
| \ | the following character is meant to be literal |
| [...] | any one of the enclosed characters (...) |
| \\(...\\) | saves pattern ... to the hold buffer |
| \n | the contents of the nth hold buffer (when replacing) |
| & | the contents of the whole matched pattern (when replacing) |
| \u,\l | change the next character to uppercase, lowercase (when replacing) |
| \U,\L | change the following text to uppercase, lowercase (when replacing) |

## Set Commands
| Command | Effect |
| --- | --- |
| ai,noai | auto indent on, off |
| ic,noic | ignore case on, off |
| nu, nonu | line numbers on, off |
| sm,nosm | show matches on, off |
