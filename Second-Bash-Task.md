# Pass Arguments to a bash Script

```
# To pass arguments to a Bash script, you can use the special variables: $1, $2, $3, # for the first, second, third arguments, and so on.
# ex:

#!/bin/bash

echo "First argument: $1"
echo "Second argument: $2"
echo "Third argument: $3"
echo "ALL Argument: $*"
```


# Global And Local Variables

```
#!/bin/bash
global_var="I am a global variable"

function my_function() {
    # Local Variable
    local local_var="I am a local variable"
    
    echo "Inside function: $global_var"  # Access global variable
    echo "Inside function: $local_var"   # Access local variable
}

echo "Outside function: $global_var"    # Access global variable
# echo "Outside function: $local_var"   # This will result in an error because local_var is not accessible here

my_function
```
Or 
```
variable1= value # this is local variable
Export variable2= value2  This is global variable
```
# Read User Input

```
#!/bin/bash

# Prompt the user for input
echo "Enter your name:"
read user_name # The read Command Used To read user Input


# Display the user's input
echo "Hello, $user_name! Nice to meet you."
```
# How to load and read arrays in Bash

```
#!/bin/bash

# Declare an array
my_array=("index0" "index1" "index2" "index3")

# Access elements by index
echo "First element: ${my_array[0]}"
echo "Second element: ${my_array[1]}"
echo "All elements: ${my_array[@]}"

```
# How to compare integers and strings in bash

**Comparing Strings:**
```
# we can use arithmetic comparison operators like '-eq' (equal), '-ne' (not equal), #'-lt' (less than), '-le' (less than or equal), '-gt' (greater than), and '-ge'       
# (greater than or equal) to compare integers. ex:

#!/bin/bash

num1=10
num2=20

if [ "$num1" -eq "$num2" ]; then
    echo "Numbers are equal"
else
    echo "Numbers are not equal"
fi

if [ "$num1" -lt "$num2" ]; then
    echo "num1 is less than num2"
fi

```

**Comparing Strings:**
```
# For string comparisons, we can use string comparison operators like '=' (equal),   # '!=' (not equal), '<'' (less than, based on ASCII values), and '>' (greater than,  # based on ASCII values). ex:
#!/bin/bash

string1="apple"
string2="banana"

if [ "$string1" = "$string2" ]; then
    echo "Strings are equal"
else
    echo "Strings are not equal"
fi

if [ "$string1" \< "$string2" ]; then
    echo "string1 comes before string2"
fi

```
# How to detect file types in Bash
```
# Using file -b
#!/bin/bash

filename="example.txt"

file_type=$(file -b "$filename")
echo "The file $filename is of type: $file_type"

```
# How to use for, while, and until loops
```
for arg in [list] ; do .... done
while [ condition ] ; do command(s)... done
until [condition] ; do ... done

examples:
# For loop
#!/bin/bash

# Example using a for loop to iterate through an array

---- 
# while
#!/bin/bash

# Example using a while loop to count from 1 to 5

counter=1

while [ "$counter" -le 5 ]; do
    echo "Counter: $counter"
    ((counter++))
done
----
#!/bin/bash

# Example using an until loop to wait until a process is finished
process_finished=false

until $process_finished; do
    # Simulate some process
    sleep 2

    if [ some_condition ]; then
        process_finished=true
    fi
done

echo "Process has finished."

```
# How to use functions in Bash
```
# First define the function
My_func()
# Then call it
My_func
example:
---
#!/bin/bash

# Define a function
say_hello() {
    echo "Hello, world!"
}

# Call the function
say_hello
---

#!/bin/bash

# Define a function that takes parameters
greet() {
    echo "Hello, $1!"
}

# Call the function with an argument
greet "Alice"
-----
#!/bin/bash

# Define a function that returns a value
add_numbers() {
    sum=$(( $1 + $2 ))
    return $sum
}

# Call the function and capture the returned value
result=$(add_numbers 5 7)
echo "Sum: $result"

```
# How to use if statements
```
if [ condition ]; then 
	statement
fi
if [ condition1 ] 
then 
command1 
command2
command3 
elif [ condition2 ] # Same as else if 
then 
command4 
command5 
else 
default-command 
fi
```
# How to use case statements
```
case "$variable" in 
"$condition1" ) 
command... 
;; 
"$condition2" )
command... 
;; 
esac
----
example:

#!/bin/bash

# Example using case statement to match patterns

day="Monday"

case "$day" in
    "Monday" )
        echo "It's the start of the week."
        ;;
    "Tuesday"|"Wednesday"|"Thursday" )
        echo "It's a workday."
        ;;
    "Friday" )
        echo "It's almost the weekend."
        ;;
    "Saturday"|"Sunday" )
        echo "It's the weekend."
        ;;
    *)
        echo "Invalid day."
        ;;
esac

```

# How to use quotes and special characters in Bash
```
# single quoutes ' ' Text enclosed in single quotes is treated literally, and no variable or command substitution occurs within them, Special characters within single quotes are not interpreted and are treated as literal characters.  like
echo 'Hello $USER'  # Output: Hello $USER
---- 
# Double Quotes " " Special characters within single quotes are not interpreted and are treated as literal characters, -   
Special characters like `$`, and `\` are interpreted within double quotes. 
like :
USER= Sabra
echo "Hello $USER"  # Output: Hello Sabra
----
for special char
- Dollar Sign (`$`): Used for variable and command substitution.
- Backslash (`\`): Escape special characters to treat them as literals.
- Heredocs: Input multiple lines of text to a command or script. like 
cat << END
This is a multiline text
that preserves formatting.
END

```
# How to perform arithmetic calculations with Bash
```
Perform arithmetic calculations in Bash using:

- expr: `result=$(expr 5 + 3)`
- let: `let result=5+3`
- Double Parentheses `(( ))`: `result=$((5 + 3))`
- `$(( ))`: `result=$((5 + 3))`
- Floating-Point: Use `bc` for floating-point arithmetic.
```

# How to use Bash redirection
```
Bash redirection allows you to control input and output:

- `>` redirects stdout to a file (overwriting).
- `>>` appends stdout to a file.
- `<` redirects stdin from a file.
- `|` (pipe) connects stdout of one command to stdin of another.
- `2>` redirects stderr to a file.
- `&>` or `2>&1` redirects both stdout and stderr to a file or merges them.

```

----
# Bash Scripts For Sed 
```
cp /etc/passwd ~/new-passwd-file
```

```
# Display lines containing "guest":
sed -n '/guest/p' ~/new-passwd-file
```

```
# Display file except the third line:
sed '3d' ~/new-passwd-file
```

```
# Display file except the last line:
sed '$d' ~/new-passwd-file
```

```
# Display file except lines containing "guest":
sed '/guest/d' ~/new-passwd-file
```

```
 # Substitute "guest" with "myguest":
 sed 's/guest/myguest/g' ~/new-passwd-file
```
# Bash Scripts For awk

```
# Print full name of all users:
awk -F: '{print $5}' ~/new-passwd-file
```

```
# Print login, full name, and home directory of all users (with line numbers):
awk -F: '{print NR, $1, $5, $6}' ~/new-passwd-file
```

```
# Print login, uid, and full name of uid > 500:
awk -F: '$3 > 500 {print $1, $3, $5}' ~/new-passwd-file
```

```
# Print login, uid, and full name of uid = 100:
awk -F: '$3 == 100 {print $1, $3, $5}' ~/new-passwd-file
```

```
# Print lines 5 to 15 from ~/new-passwd-file:
awk 'NR >= 5 && NR <= 15' ~/new-passwd-file
```

```
# Change "guest" to "myguest":
awk '{gsub("guest", "myguest"); print}' ~/new-passwd-file
```

```
# Print all information about greatest uid:
awk -F: '$3 > max_uid {max_uid = $3; line = $0} END {print line}' ~/new-passwd-file
```

```
# Get the sum of all account IDs:
awk -F: '{sum += $3} END {print "Sum of UIDs:", sum}' ~/new-passwd-file
```

```
# Get the sum of account IDs with the same group:
awk -F: '{group_sum[$4] += $3} END {for (group in group_sum) print group, group_sum[group]}' ~/new-passwd-file
```
---- 

# tr: replace uppercase letters with lowercase letters and vice versa

```
# example  
echo "Hello World" | tr 'a-zA-Z' 'A-Za-z'
```

# Sort: sort the ~/new-passwd-file on gid/uid

```
sort -t: -k3,3n -k4,4n ~/new-passwd-file ####
```
# split

The split command is used to split a file into smaller pieces. It's often used to break up large files for easier transfer or storage. The command's basic syntax is:

```
split [options] input_file [prefix]
split -b 1M fileName part
```
# uniq

The uniq command is used to filter out adjacent duplicate lines from a sorted file. The command's basic syntax is:

```
uniq [options] [input_file [output_file]]
```

For example, to display unique lines from a sorted file named data.txt, you can use:
```
sort data.txt | uniq
```

# expr

The `expr` command is used to evaluate expressions. It's often used for basic arithmetic calculations. The command's basic syntax is:

```
expr expression
result=$(expr 5 + 3)
echo "Result: $result"
```
# paste

The `paste` command is used to merge lines from different files. The command's basic syntax is:
 
```
 paste [options] [file...]
# example: to merge two files, `file1.txt` and `file2.txt`, with a tab as the separator:

paste -d '\t' file1.txt file2.txt`
```
# test
The `test` command is used to evaluate conditional expressions in shell scripts. It's often used in conjunction with `if` statements. The command's basic syntax is

```
test condition
if test -e myfile.txt; then
    echo "File exists"
fi
```

# whatis
The `whatis` command is used to display a brief description of a command from the manual pages. The command's basic syntax is:

```
whatis command
```
# whereis
The `whereis` command is used to locate binary, source, and manual page files for a command. The command's basic syntax is

```
whereis command
```
# which
The `which` command is used to locate the executable file associated with a command. The command's basic syntax is

```
which command
```

# make your ls (check for type: file/dir, permission: read/write/execute).

```
#!/bin/bash

for item in "$@"; do
    if [ -f "$item" ]; then
        type="File"
    elif [ -d "$item" ]; then
        type="Directory"
    else
        type="Unknown"
    fi
    
    permissions=""
    if [ -r "$item" ]; then
        permissions+="r"
    else
        permissions+="-"
    fi
    if [ -w "$item" ]; then
        permissions+="w"
    else
        permissions+="-"
    fi
    if [ -x "$item" ]; then
        permissions+="x"
    else
        permissions+="-"
    fi
    
    echo "Item: $item"
    echo "Type: $type"
    echo "Permissions: $permissions"
    echo "---"
done


```

# check type of data entered by the user (string , numbers, mixed).

```
#!/bin/bash

read -p "Enter some data: " input

# Check if the input is numeric
if [[ "$input" =~ ^[0-9]+$ ]]; then
    echo "Numeric input"
# Check if the input is alphabetic
elif [[ "$input" =~ ^[a-zA-Z]+$ ]]; then
    echo "Alphabetic input"
# If not purely numeric or alphabetic, it's considered mixed
else
    echo "Mixed input"
fi

```
# make 2 nested script set the value of var variable in each and display its value before and after setting (once using export and other using sourcing)

```
#!/bin/bash

echo "Hello : var = $var"

export var="With Out Sourcing"

./inner_script.sh

echo "Outer Script - After: var = $var"

-------------
inner_script.sh
-------------
#!/bin/bash

echo "Inner Script : var = $var"

```

# make a script mycat which use the option -n only

```
#!/bin/bash

line_number=1

while IFS= read -r line; do
    echo "$line_number: $line"
    ((line_number++))
done < "$1"
####
```

# make a small menu  to chose: making more to a file or cat on it or exit.
```
#!/bin/bash

while true; do
    echo "Menu:"
    echo "1. Append to a file"
    echo "2. Display file content"
    echo "3. Exit"

    read -p "Enter your choice: " choice

    case $choice in
        1)
            read -p "Enter the filename: " filename
            read -p "Enter text to append: " text
            echo "$text" >> "$filename"
            echo "Text appended to $filename"
            ;;
        2)
            read -p "Enter the filename: " filename
            if [ -f "$filename" ]; then
                cat "$filename"
            else
                echo "File not found"
            fi
            ;;
        3)
            echo "Exiting"
            break
            ;;
        *)
            echo "Invalid choice"
            ;;
    esac
done

```

# make a menu for data entry : check data type validity.
```
#!/bin/bash

while true; do
    echo "Data Entry Menu:"
    echo "1. Enter numeric data"
    echo "2. Enter alphabetic data"
    echo "3. Exit"

    read -p "Enter your choice: " choice

    case $choice in
        1)
            read -p "Enter numeric data: " data
            if [[ "$data" =~ ^[0-9]+$ ]]; then
                echo "Valid numeric data"
            else
                echo "Invalid data"
            fi
            ;;
        2)
            read -p "Enter alphabetic data: " data
            if [[ "$data" =~ ^[a-zA-Z]+$ ]]; then
                echo "Valid alphabetic data"
            else
                echo "Invalid data"
            fi
            ;;
        3)
            echo "Exiting"
            break
            ;;
        *)
            echo "Invalid choice"
            ;;
    esac
done

```

# display all the arguments to a script in large size
```

#!/bin/bash

echo "Arguments passed to the script in large size:"
echo "-------------------------------------------"

for arg in "$@"; do
    echo "    $arg"
done

echo "-------------------------------------------"
echo "Display complete."
########
```

# Display the total number of arguments in large size.
```
#!/bin/bash

count="$#"

echo "Total number of arguments: $count"

echo "Arguments passed to the script:"
echo "--------------------------------"

for arg in "$@"; do
    echo "    $arg"
done

echo "--------------------------------"
echo "Display complete."

```
# promptuser -> if string print Hello , if number add 10
```
#!/bin/bash

read -p "Enter something: " input

if [[ "$input" =~ ^[0-9]+$ ]]; then
    result=$((input + 10))
    echo "Result: $result"
elif [[ "$input" =~ ^[a-zA-Z]+$ ]]; then
    echo "Hello"
else
    echo "Mixed input"
fi

```
