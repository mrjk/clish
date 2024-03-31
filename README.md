# Clish

Portable Bash Command Line framework.

## Quickstart

Open your favorite text editor and paste:
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
  : "meta=NAME [FILE]"

  echo "Name: $1"
  echo "File: $${2:-<NO_FILE>}"

}

# Import live clish
CLISH_URL='....'
CLISH_LIB=/tmp/clish-$(id -u)
. $CLISH_LIB 2>/dev/null || { curl -s "$CLISH_URL" -o $CLISH_LIB && . $CLISH_LIB ; }
clish_init "$@"
```
