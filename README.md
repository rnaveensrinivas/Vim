# Introduction
* Vim is difficult to learn, hence you need strong motivation to learn and discipline to stay consistent.
* You might get stuck, you might think of giving up, you might think Vim is too hard. **Dont' wish Vim was easier, wish you were better!**
* Here are two uncomfortable truths: 
  * Skills take time and effort to master.
  * Many things aren't fun until you're good at them.
* When learning something there is a period of time in which you're horribly unsklled, and you're painfully aware of that fact. 
* If you invest time and energy to learn Vim concepts, you will be in the **top 5%** of human population when it comes to productivity in coding, programming, and text editing.
> Bram Moolenaar, the creator of Vim, wrote:  
> “Learning to drive a car takes effort. Is that a reason to keep driving your bicycle? No, you realize you need to invest time to learn a skill. Text editing isn’t different. You need to learn new commands and turn them into a habit.”

* *Detour*: three important learning principles: 
  1. Pareto Principle, 80/20 principle
  2. Mini Habits
     * mini habits help you stay consistent, and reduce friction
     * keep small achievable goals, eg. 1 typing test a day. 
  3. Improve 1% every day   

# Vim Basics
## Vim Philosophy
* The two main ideas of Vim that make them different are, **modal editing** and **operators**
* **Modal Editing**
  * One spends majority of the time editing and review code here and there rather than typing.
  * Hence Vim heavily optimizes navigation. Eg, In command mode, pressing `gg`, takes you to top of file.    
* **Operators**
  * They are used to delete, change or insert text, copy or format it. 
  * For eg, you want to delete from current word to EOL, press `d$`. 
  
## Starting Vim
* Starting vim in command line: 
  ```bash
  $ vim
  ```
* Command line arguments for Vim: 
  * `+NUM` - position cursor at that line.
  * `+/{pattern}` - position curson at the first line that matches pattern
  * `+cmd` - an Ex command, executed after the first file has been read.
  * `-x` - use encryption to read or write files. 
  * Some examples: 
    ```
    $ vim +36 myFile.txt
    $ vim myFile.txt "+446d|x" # delete the line 446
    ```
## First Vim Session
* To rum Vim, open terminal and type, `vi` or `vim`. 
* You will start in Normal mode. 
* To fill it with content, switch to insert mode, press `i`.
* To get back to Nomral mode, press `Esc`.
* To type a command in Normal mode, you need to use `:`.
* For eg, save and exit Vim is, `:wq <filename>` (since you started as vim, you need to give filename) - `w` mean write and `q` means quit. To quit without saving use `:q!`
  
# Vim Concepts
## Modes
* Vim has got 12 modes in total, Normal Mode, Insert Mode, Visual Mode, Command-Line Mode, Replace Mode, Select Mode, Ex Mode, Operator-Pending Mode, Insert Normal Mode, Terminal Mode, Command Mode, and Shell Mode.
* But one mostly uses the following the most, Normal Mode, Insert Mode, Command Mode, Visual Mode, and Insert Normal Mode.
### Normal Mode
* Vim starts in this mode.
* Used for navigation and text manipulation.
* A good habit: whenever you're not typing, it's better to get back to Normal mode. 
* To get into Normal mode, press `Esc`.
### Insert Mode
* Used for content management.
* To get into Insert mode, press `i`.
* By default, `-INSERT-` is shown at the bottom left of Vim window.
### Command Mode
* Used for running Ex commands. 
* To enter this mode, type `:` in Normal mode.
* After running the command, Vim returns to Normal mode.
### Visual Mode
* For navigation and manipulation of text selection. 
* The movement commands extends to highlighted areas.
* When a non movement command is used, it's executed for the highlighted area.
* By default, `-VISUAL-` is shown at the bottom left of Vim window.
### Insert Normal Mode
* Used for executing one command when in Insert mode. 
* To enter this mode, press `Ctrl-o`, enter the command. 
* After executing the command Vim returns to insert mode. 
* By deafult, `-(insert)-` is shown at the bottom left of Vim window. 

# Commands
* In general there are three ways of executing commands in Vim

### Ex Commands
* Any command that runs as `:{command}`, for eg. `:help`
* To see all the possible Ex commands, type `:help ex-cmd-index`
### Mapped Commands
* A complex command that we map with some key for ease of use. 
* They are usually added in `.vimrc` file. 
### Editing Commands
* Commands that you normally use in Normal and Insert modes. 
* Eg, `d4w`

# Working with Files
## Opening files
* When you open an existing file, the content of the file is loaded in the Vim buffer. 
* Buffer is a piece of memory that's been loaded with content of a file.
* We don't use "current opened file", but "current buffer."
* There are two ways to open files in vim. 

### Opening from terminal
```bash
$ vim <filename>
```
### Opening file from Vim
* When opening vim, no file will be loaded, by default.
```bash
$ vim

# within vim, using the command mode.
:e <filename>
```
### Getting contents from another file
* A long way is described below: 
```bash
$ vim

# loding the first file into vim buffer
e: <filename_1>

# now we want content from another file
e: <filename_2>

# copy content Ctrl-Shift-C
# go back to <filename_1>
e: <filename_1>

# paste content Ctrl-Shift-V
```
* There is an alternative way of doing it, using `:r[ead]` Ex command.

```bash
$ vim

# loding the first file into vim buffer
e: <filename_1>

:r[ead] <filename_2> # appends to cursor position
```
| Ex Command            | Description                                |
|-----------------------|--------------------------------------------|
| `:r <file>`             | Insert below current cursor                |
| `:0r <file>`            | Insert before first line                   |
| `:r!sed -n 2,8p <file>` | Insert liens 2 to 8 from file below cursor |
| `:r !ls`                | Insert directory listing below cursor      |
* `!sed -n 2,8p <file>` is a prompt
  * `sed` stands for stream editor
  * `-n` prevents printing all the lines, since sed print all the lines by default. 
  * `2,8p` print the lines 2 to 8
* To append to end of file, simple move the cursor to end, by pressing `G` and then `:r[ead] <file>` Ex command

### Tips: 
* You can open a file whose name (or path) is currently under the cursor using `gf` (goto file) command in Normal mode. 
* You can open a link whose link is currently under the cursor using `gx` command in Normal mode. 
  
## Closing files
| Command     | Description   |
|-------------|----------|
| `:wq`       | Save currently opened file and exit Vim (even if the file is not changed). **Last change date modified.**|
| `:x`        | Exit Vim but write only when changes have been made. **If no changes were made then last modified date is unaffected.**|
| **`ZZ`**| **Equivalent to `:x`. Notice there’s no `:`. This is a key press.** |
| `:q`| Exit Vim. Fails if we have made some changes to the file|
| `:q!`| Exit Vim without saving currently opened file.|
| `:qa` | Exit all open files in the current Vim session. Fails if any of the file is modified|
| `:qa!` | Exit all open files in the current Vim session disregarding all changes|
* Use `ZZ` it's quick and doesn't mess up the last modified date of the file. 
  
## Saving files
* When we save, we **W**rite the content of the Vim buffer to the disk.

  | Command  | Description|
  |------|---------------|
  | `:w`| Save currently opened file (which was previously saved).|
  | `:w file.txt`  | Save currently opened file as `file.txt`. Fails if `file.txt` alredy exists. |
  | `:w! file.txt` | Save file as `file.txt` with overwrite option.|
  | `:sav file.txt`| Save current buffer as a new file `file.txt`. Same as `:w`|
  | `:up[date]`    | Like `:w` but only saves when the buffer has been modified.|
* `:w` commands update the last modified date of the file. 
* `:up[date]` updates the last modified date only if there are changes. **Preferred** 

## Navigation
### Basic Movement
* Can use arrow keys to navigate, but this moves the fingers from home row. 
* Hence use `h => left`, `j => down`, `k => up`, `l => right`. 
* Once you get used to navigating with `hjkl`, you become very efficient. 
### Navigate through words
* Before we see the navigation shortcuts, we need to understand what exactly is a word. 
  * `WORD` => sequence of non-blank characters delimited by **white space**.
  * `word` => sequence of non-blank characters delimited by **non-keyword characters** such as `,`, `.`, `-`, `[` etc. Useful when going through source code.
  * For example, `Vim "navigation" is not-so difficult!`
    * Number of `WORD`s = 5
    * Number of `word`s = 10
* Navigation shortcuts

  | Key | Description          |
  |-----|------------------------------------------|
  | `w` | Go to the start of the next word         |
  | `W` | Go to the start of the next WORD         |
  | `e` | Go to the end of the current word        |
  | `E` | Go to the end of the current WORD        |
  | `b` | Go to the previous (before) word         |
  | `B` | Go to the previous (before) WORD         |
* All these shortcuts can take a number as prefix. eg. `3w` and `6j`.
  
### Scrolling pages

| Shortcut | Description                                     |
|----------|-------------------------------------------------|
| `Ctrl-d` | Scroll down half a page                        |
| `Ctrl-u` | Scroll up half a page                          |
| `Ctrl-f` | Scroll down a full page (or forwards)          |
| `Ctrl-b` | Scroll up a full page (to the beginning, or backwards) |

### Jumping around the file

| Command | Description                                     |
|---------|-------------------------------------------------|
| `gg`    | Go to the top of the file                      |
| `G`     | Go to the bottom of the file                   |
| `{`     | Go to the beginning of the current paragraph   |
| `}`     | Go to the end of the current paragraph         |
| `%`     | Go to the matching pair of `()`, `[]`, `{}`    |
| `50%`   | Go to the line at 50% of the file              |
| `:NUM`  | Go to line `NUM`. For example, `:28` jumps to line 28 |

### Navigating inside the current window

| Command | Description                                       |
|---------|---------------------------------------------------|
| `H`     | Move cursor to the first (highest) line in the current window. |
| `L`     | Move cursor to the lowest line in the current window.          |
| `M`     | Move cursor to the middle of the current window.              |

### Navigating in insert mode
* You shoudn't navigate in insert mode. Press `Esc` go to normal mode, navigate and then press `i` to get into insert. 
    
  | Shortcut | Description                                       |
  |---------|---------------------------------------------------|
  | `Shift-Right-Arrow`   | Go to the right, word by word. |
  | `Shift-Left-Arrow`   | Go to the right, word by word. |

### Tip
* When in Insert mode, press `Ctrl-o` to get back to Normal mode and execute **one** command, after which you'll be auto directed to Insert mode. 

## Basic search
* All search operations are done in Normal mode. 
* Search forward by typing `/`, a pattern, then `Enter`. 
* In search press `n` for forward search, `N` for backward search.
* To make first match, go to top of file `gg`, then match `n`. 
* To make last match, go to bottom of file `G`, them match `N`. 
* Search backward by typeing `?`, a pattern, then `Enter`. Here `n` (backward) and `N` (downward). 
* To quit search press `Esc`. 

### Search for current word
* Place your cursor on any word and,
  * press `*`, to find next occurence of exact word
  * press `#`, to find previous occurence of exact word
  * press `g*`, to find next occurence of a word that contains cursor word
  * press `g#`, to find previous occurence of a word that contains cursor word

### Search history
* Type `/` or `?`, then use up or down arrow keys to navigate. 
* To search similar word under the cursor without manullay typing the word, press `/` + `Ctrl-r` + `Ctrl-w`. 
* Cursor history can be traversed using `Ctrl-O` (jump backward) and `Ctrl-i` (jump forward)
* If you want to repeat the previous search pattern, just type `/` and `Enter`. An empty search patternwill repeat the last search.
* For all the searches above, we can prefix a number, which denotes how many we would like to skip. Eg. `6/pattern`, `5*` of current word etc.

## File Manager (netrw) in Vim
* netrw is a built-in plugin for Vim (and its fork, Neovim) that provides file browsing and file management capabilities. 
* It allows users to explore directories, open files, and even work with remote files over protocols like FTP, SFTP, SCP, or HTTP.
* Launching netrw: 
  * `:Ex` - **Ex**plore - open current directory in current Vim windows.
  * `:Ex <dir>` - open specified directory `<dir>`
  * `:Sex` - open current directory in horizontal split
  * `:Vex` - open current directory in vertical split
  * `:Tex` - open current directory in new tab
  * `:Lexplore` - open current directory in vertical split on the left. 
* Try out `:40vs +Ex`
  * Try to break down the command
  * `:40vs`
  * `:40vs +Ex`
* Try out various options shown when in `:Ex` directory. Eg. `i`, `s` etc.
* `i` gives various views - thin, long, wide, and tree. 
* If you have a favorite view, you can set it permanently using, `let g:netrw_liststyle = 3` in `.vimrc` file.  
* Also, to go through history, just press `:` and then up/down arrow keys. 
### Changing how files are opened
* We can open directories with Vim. 
  ```bash
  vi ~
  ```
* Displays all the files in the directory.
* This actaully outputs `netrw`. 
* Some basic operations:
  * `Enter` - open file or enter directory under cursor. 
    * the file will be opened in the same window as netrw, not practical. To have it as side split, and to load files in another split, we need to change `netrw_browse_split` option. To make things permanent add `let g:netrw_browse_split = 4` in `.vimrc`.
    * Also, we can set the netrw window split using `netrw_browse_split`, for eg. `let g:netrw_winsize = 20` sets width of netrw split to 20% of Vim window.
  * `D` - delete file under cursor.
  * `R` - rename the file under cursor.
  * `X` - execute the file under cursor.
  * `%` - opens a new file in the current directory, Vim will ask you for a name and open a buffer.
  * **what about the above operations for a directory?**
  * **skipping the section `Editing files via SSH`**