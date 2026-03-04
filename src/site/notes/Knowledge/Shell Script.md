---
{"dg-publish":true,"permalink":"/knowledge/shell-script/","tags":["shell","script","posix-shell"]}
---

---

## Info

- Place in `/usr/local/bin` to access easily
- Add `#!/bin/sh` to the top of the file, t  hen you don't have to add a file ending

## Variables

```sh
variable="I am a variable"
other_variable=123

echo "My variables: $variable, $other_variable"

readonly_variable="xyz"
readonly readonly_variable

unset variable
```

## User Input

```sh
# Access number of arguments
if [ $# -eq 0 ]; then
    echo "No arguments supplied"
fi

# Access specific arguments
first_arg=$1
second_arg=$2       

# Reading Input
read -p "Enter input: " user_input
```
