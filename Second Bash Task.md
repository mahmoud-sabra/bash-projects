# Pass Arguments to a bash Script

```
# To pass arguments to a Bash script, you can use the special variables: $1, $2, $3, # for the first, second, third arguments, and so on.
ex:

#!/bin/bash

echo "First argument: $1"
echo "Second argument: $2"
echo "Third argument: $3"

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
for arg in [list] ; do
while [ condition ] ; do command(s)... done
until [condition] ; do ... done

examples:
# For loop
#!/bin/bash

# Example using a for loop to iterate through an array
fruits=("apple" "banana" "cherry" "date")

for fruit in "${fruits[@]}"; do
    echo "Fruit: $fruit"
done

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
    "Monday")
        echo "It's the start of the week."
        ;;
    "Tuesday"|"Wednesday"|"Thursday")
        echo "It's a workday."
        ;;
    "Friday")
        echo "It's almost the weekend."
        ;;
    "Saturday"|"Sunday")
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