# Bash Shell and Scripts

## Philosophy 

There are a number of factors which can go into good, clean, quick, shell scripts.

- it must be clear and readable
- avoid unnecessary commands

Advantages to not writing code that appears as "black magic"

- it is likely the script will grow so even if it's small now write it well
- if nobody else understands the code you will be lumbered with maintaining it forever

## Script File Basics

Each script file starts out with `#!` which is called "shebang". What follows the pound bang (aka: shebang), is the path name to the program to run to interpret that script.

*Naming*

It is common practice to end the file with _.sh_ but not required. 

### Simple Example

_Users/Isaac/shells_

```
cd ~
mkdir shells
> firstattempt.sh
nano firstattempt.sh
```

```
!#/bin/bash
cd ~/Documents/
mkdir 'thisisatest'
```

```
chmod +x firstattempt.sh
```

```
./firstattempt.sh 
```

In order to run firstattempt.sh anywhere, it must be added to the PATH var,
otherwise you have to be where the file lives. 

## Sourcing Scripts 

If you run your script using `./firstattempt.sh` it executes in a new shell (one which you never actually see)

Another way to execute a shell script is to source it.

`source firstattempt.sh` or `. ./firstattempt.sh`

which uses the current shell. 

When sourcing you have access to aliases created in your profile, and also variables defined within the script itself.

## Custom Commands

To have it setup so when `firstattempt` is typed into the terminal that it runs:

1. create a bin directory in user root directory

  ```
  cd ~
  mkdir bin
  ```
2. update bash_profile to include new path
3. copy bash scripts into that folder `bin`
4. reload terminal 
5. type filename (e.g. firstattempt)

## Variables 

Are defined like `isaac=meals`

If there is a space before the = it would think ```isaac``` is a command.
same if there was a space after =. so it's important to not have spaces.

If there are spaces in the value then surrend it by  double qoutes. `name="isaac meals"`

Same applies for special characters; they, too, should be wrapped in double qoutes.

To remove variables from memory use the `unset` command. 

To get the value of a variable add a `$` before the name `echo $name`

If the variable will be used outside the process then add `export` before the variable name like `export name="isaac meals"` this will create a copy (NOT SHARING BY REFERENCE)

### Prompt, Store Values, Concat

To prompt for and then store values use `read`

```
!#/bin/bash
echo "What is your name?"
read NAME
echo "Hello ${NAME}"
```

_`read` command automatically places quotes around its input, so that spaces are treated correctly_

### Grouping / Scope 

If variables are grouped by () then it creates a new processes. Once it is closed those variables or values are no longer accessible.

If grouped by {} then it will still be accessible after it is closed.

```
a = 1
(
  a = 2
)
echo $a 
# prints 1
```

```
a = 1
{
  a = 2
}
echo $a 
# prints 2
```

***functions bc they use {} don't get a _copy_, will modify variables on a global scope basis***


### Bult-in Variables

_not a complete list but useful ones to be aware of_

| variable | Description |
| -------- | ----------- |
| $PWD     | displays present working dir |
| $HOSTNAME | displays hostname |
| $HOME     | user's home dir |
| $USER     | username |
| $EUID     | userid |
| $GROUPS   | GID info |
| $HOSTTYPE or $MACHTYPE | host architecture ie 32bit or 64 bit |
| $OSTYPE | gets the OS |
| $RANDOM | get a random number |
| $LINENO | gets the present line number the script is on |
| $0 | gives script name |
| $1 .. $9 | are the first 9 additional parameters the script was called with |
| $@ |  all parameters $1 .. whatever |
| $* | similiar to $@ but does not preserve any whitespace |
| $? | error or exit status |
| $# | number of params |

_general rule, use $@ and avoid $*._

for more: http://www.tldp.org/LDP/abs/html/internalvariables.html

## Escape Characters

", $, `, and \ are still interpreted by the shell, even when they're in double quotes. 

The backslash character is used to mark these special characters so that they are not interpreted by the shell.

Special Characters

## Test Command

`test <EXPRESSION>` or `[ <EXPRESSION> ]`

This command allows you to do various tests and sets its exit code to 0 (TRUE) or 1 (FALSE) whenever such a test succeeds or not.

for more info: http://wiki.bash-hackers.org/commands/classictest

## Functions

## Control Flow

### IF

### Case 

### For Loops

```
for i in 1 2 3 4 5
do
  echo "Looping ... number $i"
done
```

https://www.cyberciti.biz/faq/bash-for-loop/

### While Loops

```
INPUT_STRING=hello
while [ "$INPUT_STRING" != "bye" ]
do
  echo "Please type something in (bye to quit)"
  read INPUT_STRING
  echo "You typed: $INPUT_STRING"
done
```

This will run indefinitely until you type "bye" when prompted.



## Unit Testing

https://github.com/kward/shunit2

Install: `brew install shunit2`

Create basic test

```
testEquality()
{
    assertEquals 1 1
}
```

```
shunit2 firstattempt.sh
```

```
testEquality

Ran 1 test.

OK
```

or if you mess up and there is a failure 

```
testEquality
ASSERT:expected:<1> but was:<13>

Ran 1 test.

FAILED (failures=1)
```

