# Clish

Portable Bash Command Line framework, with annotations à la Click

## Quickstart

Open your favorite text editor and paste in `myscript`:
```
#!/bin/bash

# Define your commands
cli__hello ()
{
  : "help=Show word string"
  echo "World"
}

cli__test1 ()
{
  : "help=Show word string"
  : "args=NAME [FILE]"

  [[ "$#" != 0 ]] || _script_die 6 "Missing name for command: test1"
  
  echo "Name: $1"
  echo "File: ${2:-<NO_FILE>}"
}

# Import live clish
CLISH_URL='https://raw.githubusercontent.com/mrjk/clish/main/clish.bash'
CLISH_LIB=/tmp/clish-$(id -u)
. $CLISH_LIB 2>/dev/null || { curl -s "$CLISH_URL" -o $CLISH_LIB && . $CLISH_LIB ; }
clish_init "$@"
```

Ensure your script is executable:
```
chmod +x myscript
```

Show help command, it comes with some default commands:
```
$ ./live_app.sh -h
live_app: Command line tool to run stuffs

usage: live_app.sh [<OPT>,..] <COMMAND> 
       live_app.sh help

options:
  -h                             Show this help
  -n                             Enable dry mode
  -f                             Enable force mode
  -v  DEBUG|INFO|WARN            Set verbosity
  -m  TEXT                       Set text message with spaces

commands:
  completion                     Show bash completion script
  example                        Example command
  hello                          Show word string
  help                           Show this help
  hook [SHELL]                   Show shell hook
  test1 NAME [FILE]              Show word string

info:
  author: author <email@address.org>
  version: 0.0.1-alpha (2024-03-30)
  license: GPLv3
  website: https://github.com/author/live_app

```

You can test them:
```
$ ./live_app.sh hello
World
$ ./live_app.sh test1 MY_NAME
Name: MY_NAME
File: <NO_FILE>
$ ./live_app.sh test1 MY_NAME MY_FILE
Name: MY_NAME
File: MY_FILE
$ ./live_app.sh test1 ; echo "Coammnd failed with exit: $?"
  DIE: Missing name for command: test1
Coammnd failed with exit: 6
```

Supported annotations for command functions:
* `help`: Help message
* `arg`: Arguments in help message


## Other helpers

TODO


## Internal functions



