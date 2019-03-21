# Git Tips & Tricks
Cool stuff to do neat things with @allthedoll on March 21, 2019

## Git colors
`git config --global color.ui auto`
This literally just ensures that git is colorized

### About
- color.ui is the master switch for git colors; you can set it to "false"
- Basic colors: black, red, green, yellow, blue, magenta, cyan, & white
- ANSI 256 colors (0-255)
- RGB colors as hexadecimal if your terminal supports it
- Themes available, like Nord: https://github.com/arcticicestudio/nord

### Try it out
- `git config --global color.ui false --replace-all`
  -  Returns you to a bland, colorless world
  - Run `git log` and note the lack of color
  - Return to a fun, colorful world with `git config --global color.ui auto`
  - Celebrate with `git log` that has color in it


## Git log graph
Creates a visual log

### About
- Graph option makes it visual
- Pretty=format:’string’ to specify colors and decorations
- Pretty also comes in oneline, short, medium, full, fuller, email, & raw
- Decorations include: bold, dim, blink, ul (underline), and reverse (swap foreground and background)
- Note that not all options will be available for each pretty type specified
- Plceholders
  - %C is color
  - %h is abbreviated commit hash
  - %Creset is reset color
  - %d decorate
  - %s is subject
  - %cr is committer date relative
  - %an is author name
- More information: https://git-scm.com/docs/pretty-formats

### Try it out
- ANSI basic colors
`git log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit --date=relative`

- ANSI 256 colors
`git log --color --graph --pretty=format:'%C(92)%h%Creset -%C(255)%d%Creset %s %C(220)(%cr) %C(45)<%an>%Creset' --abbrev-commit --date=relative`

- RGB as hexidecimal
`git log --color --graph --pretty=format:'%C(#9873b5)%h%Creset -%C(#0077be)%d%Creset %s %C(#ec3b83)(%cr) %C(#20b2aa)<%an>%Creset' --abbrev-commit --date=relative`


## Git log ...log (-L)
`git log -L <start>,<end>:FILE`
Allows you to see all of the log entries that involve a diff of this file between the start and end lines

### Try it out
- Change directory into `allthedoll/git`
- `git log -L 15,20:users.ldif.j2`
- Change the line numbers around
- Try with other files in other repos

## Git aliases
Make custom shortcuts with `git config --global alias.nickname “command”`
- You can combine actions in aliases with && 

### Try it out
- `git config --global alias.logp "git log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit --date=relative"`


## Git status
Check your staging status

### Try it out
- See the visual difference between running
  - `git status`
  - `git status -sb`

## Search your command line history
Forgot what that one thing you did earlier was? Me too.

### About
- Unix: control+R
- Windows: F7

### Try it out
- Search for `ldif`
  - Did it find `git log -L 15,20:users.ldif.j2`? Why or why not?


## Git grep
You can search git history with grep! 

### About
- You can get very specific in your searches

Example: `git grep 'time_t' -- '*.[ch]'`
- Finds where time_t is in a file ending in .c or .h

### Try it out
Change directory into `allthedoll/git`
`git grep 'superman' -- '*.j2'`
- Finds .j2 files containing the word "superman"


## Git autocorrect
Typo much? No problem.

### About
Git can save you from having to retype things you have mistyped!

### Try it out
- Run `git config --global help.autocorrect 10` to set up an autoccorect; here we've set it to correct after one second
  - Note the number specified before it autocorrects is in tenths of a second
- Try `git sttaus`


## Git patch
Allows you to stage portions of files, known as `hunks`
- A hunk is each section of a diff that shows some context on where the differences happen

### About
`git add -p` (instead of `git add` once you've modified a file or files)
- Cool if you need to push a feature but also have a bug
- Option available:
  - y - stage this hunk
  - n - do not stage this hunk
  - q - quit; do not stage this hunk nor any of the remaining ones
  - a - stage this hunk and all later hunks in the file
  - d - do not stage this hunk nor any of the later hunks in the file
  - g - select a hunk to go to
  - / - search for a hunk matching the given regex
  - j - leave this hunk undecided, see next undecided hunk
  - J - leave this hunk undecided, see next hunk
  - k - leave this hunk undecided, see previous undecided hunk
  - K - leave this hunk undecided, see previous hunk
  - s - split the current hunk into smaller hunks
  - e - manually edit the current hunk
  - ? - print help

### Try it out
- cd into the `git` repository we've been using if you aren't there
- Make changes to the `users.ldif.j2` file across multiple lines and save it
- `git add -p`
- Choose an option (detailed above)
- Play around and see what it does
- Note that `e` and `s` for edit and split mode are both very granular
  - Lines with**+** are new lines,- indicates deleted lines and lines with a space**’ '** are left untouched
  - You can make hunks smaller in split mode
  - You can delete the lines you don’t want to include and then modify the number of lines on the “to-file-range”
  - Line numbers matter, and any additions or deletions warrant modifications

## Git config notes
### Git config levels
- `--system`
  - System-wide configurations; they apply to all users on this computer
- `--global`
  - User-level configurations; they only apply to your user account
- `--local`
  - Repository-level configurations; they only apply to the specific repository where they are set

## Stuff you should definitely have in your `.gitconfig`
`.gitconfig` is the file that Git uses to operate and configure variables

### About
You can customize the way git looks and acts by customizing your `.gitconfig`

### Try it out
- View what you have by opening the `.gitconfig` or run `git config --list`
- At minimum, you should definitely have
  - `git config --global user.name "First Last"`
  - `git config --global user.email "you@email.com"`
  - `autocrlf` (auto carriage return line feed) // This option tells git to not track line changes in git, which can vary OS to OS
    - For Windows users: `git config --global core.autocrlf true`
    - For Unix: `git config --global core.autocrlf input`
