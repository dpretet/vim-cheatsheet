# [All the right moves](https://vim.fandom.com/wiki/All_the_right_moves)

Vim is very keyboard centric and provides many ways to move the cursor.
Becoming familiar with them leads to more effective text editing.

Here is the basic to move around the text in normal mode, we should be your
default to edit text:

    h   move one character left
    j   move one row down
    k   move one row up
    l   move one character right
    w   move to beginning of next word
    b   move to previous beginning of word
    e   move to end of word
    ge  move to end of previous word
    W   move to beginning of next word after a whitespace
    B   move to beginning of previous word before a whitespace
    E   move to end of word before a whitespace

All the above movements can be preceded by a count; e.g. `4j` moves down 4
lines, or `4w` to jum to the next 4th word.

Follow other ways to move in the buffer:

    0   move to beginning of line
    $   move to end of line
    _   move to first non-blank character of the line (or ^)
    g_  move to last non-blank character of the line
    gg  move to first line
    G   move to last line
    ngg move to n'th line of file (n is a number; 12gg moves to line 12)
    nG  move to n'th line of file (n is a number; 12G moves to line 12)
    H   move to top of screen
    M   move to middle of screen
    L   move to bottom of screen

Ctrl key can also be used, but here to move the screen:

    Ctrl-D  move half-page down
    Ctrl-U  move half-page up
    Ctrl-B  page up
    Ctrl-F  page down
    Ctrl-O  jump to last (older) cursor position
    Ctrl-I  jump to next cursor position (after Ctrl-O)
    Ctrl-]  to jump to variable/function/class definition with thge help of
            ctags file (could be remapped to ctrl-t with `nmap <C-T> <C-]>`)

Ctrl-i & Ctrl-o can be used to move between buffers, if you jumped to a new
one with edit command or with tags.

The search command is a powerfull method to move across the buffer:

    /foo    search for next 'foo' pattern
    ?foo    search for previous 'foo' pattern
    ctrl-g  jumps to the next occurrence of the pattern (if didn't hit enter)
    ctrl-t  jumps to the previous occurrence (if didn't hit enter)
    n       next matching search pattern
    N       previous matching search pattern

Another easy ways to search for a word:

    *       next whole word under cursor
    #       previous whole word under cursor
    g*      next matching search (not whole word) pattern under cursor
    g#      previous matching search (not whole word) pattern under cursor
    gd      go to definition/first occurrence of the word under cursor
    %       jump to matching bracket { } [ ] ( )

t/f keys are great to navigate into a line:

    fX   to next 'X' after cursor, in the same line (X is any character)
    FX   to previous 'X' before cursor (f and F put the cursor on X)
    tX   til next 'X' (similar to above, but cursor is before X)
    TX   til previous 'X'
    ;    repeat above, in same direction
    ,    repeat above, in reverse direction
    
Vim embeds a bookmark system, pretty handy to use:
    
    m {a-z A-Z}      Set bookmark {a-z A-Z} at the current cursor position
    `{a-z A-Z}       Jumps to the bookmark {a-z A-Z}
    :marks           List all bookmarks

Treat yourself! To learn vim, loose the habit to use arrow keys in normal mode:

```vim
noremap <Up> <NOP>
noremap <Down> <NOP>
noremap <Left> <NOP>
noremap <Right> <NOP>
```

The goal is not really to substitute arrow keys with only h/j/k/l but better
rely on movement like w/e/b to move across the text.

You should also rely as much as possible also on relative line number to speed
up your moves:

```vim
" Display absolute and relative line number
set nu rnu
```

Instead of typing n times k or j to move up and down the cursor, just
type `4j` to move down to four lines, by easily get the move number from the
left sidebar.

Another nice improvement while Vim is very keyboard centric is to disable the
mouse, at least in insert mode. This enforces the habit to go back and forth
the normal mode and use built-in Vim motions.


```vim
" setup the mouse only for normal mode:
set mouse=n
```

That's the beginning of ninja editing ^^


# [Vim as a language](https://benmccormick.org/2014/07/02/learning-vim-in-2014-vim-as-language)

Vim proposes several commands to modify the text in normal mode. Normal mode
should be considered as the default mode to edit the buffer once the text has
been written and then simply need to be modified and adapted.

Commands can be grouped in two ways:

One character command:

    x   delete character under the cursor
    s   delete character under the cursor and enter insert mode
    r   replace character under cursor with the next key stroke

We treat the buffer a single charachter at a time, deleting for instance few
letters and then move to next or previous words with w/e/b. These commands
can be also prefixed with number to apply the change to the next `n` chars.

    4x      delete the next 4 chars
    2ra     replace the two next chars with `a`
    3s      delete the next 3 chars and enter insert mode

The second group of commands operates on object, and must be associated with
movements. This can be viewed as a kind of editing language, with verb
(the command) and the subject (the motion).

    d       delete
    c       delete and enter insert mode
    y       yank (copy)

    dd      delete the whole line
    cc      delete the line and enter in edit mode
    yy      copy the whole line

Here is an example to combine command (verb) and movement (subject):

    cw      delete the word under cursor until next space and enter edit mode
    ciw     same as `cw` but apply on the complete word under cursor
    caw     same as `ciw` but if on space apply on next word

These combinations can be applied also with `d` and `y` command. You can also
operate in sentence and paragraph:

    dis     delete the complete sentence
    dip     delete the complete paragraph

You can also combine with search command:

    dta     delete the characters until the next `a` (excluded)
    dya     delete the characters until the next `a` (included)


# g command

g is an important Vim command, learn it to unleash your flow:

    ge      Move to end of previous word
    gq      Wrap selected text to match to max line length
    gf      Open file name under the cursor


# Misc.

- Interesting
[answer](https://gist.github.com/dpretet/7ab642f06dfbcdd9972cf94be9ea0033)
by Jim Dennis on Stack Overflow
[question](http://stackoverflow.com/questions/1218390/what-is-your-most-productive-shortcut-with-vim/1220118#1220118)

- [Vim as language](https://benmccormick.org/2014/07/02/learning-vim-in-2014-vim-as-language)

- [Vim text objects](https://blog.carbonfive.com/vim-text-objects-the-definitive-guide/)

- [All the right moves](https://vim.fandom.com/wiki/All_the_right_moves)

- [Seven habits of effective text editing](https://www.moolenaar.net/habits.html) by Bram Moolenaar

- [Vim Regex](http://vimregex.com/)

# Write Plugins

Vim is very extensible and provides tons of APIs to write custom plugins to
enhance it. Follow two great resources by Steve Losh:

- [Learn Vimscript the Hard Way](https://learnvimscriptthehardway.stevelosh.com)
- [Writing Vim plugins](https://stevelosh.com/blog/2011/09/writing-vim-plugins/)
