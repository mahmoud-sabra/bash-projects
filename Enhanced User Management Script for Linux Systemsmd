.## 1. To know the path of bash shell type 

```
which bash
```

## 2. Then add it at the top of your script 
``` 
#! /bin/bash
```

## 3. Check the script is being run by root user, if not will exit
```
#! /bin/bash
# Check if the user is root or not
if [ "$(id -u)" != "0" ]; then
	echo "This sript must run by root" 
	exit 1
fi
```
or 
```
#! /bin/bash
# Check if the user is root or not
if [ "$EUID" -ne 0 ]; then
	echo "This sript must run by root" 
	exit 1
fi
```

## 4. Ask the user how many accounts he wants to add
```
#! /bin/bash
# Check if the user is root or not
if [ "$EUID" -ne 0 ]; then
	echo "This sript must run by root" 
	exit 1
fi
# Ask how many accounts he wants to add 
read -p "How many accounts you want to add? : " NumAccounts
```
## 5. Calculate and print the total number of users before and after adding operation.
```
#! /bin/bash
# Check if the user is root or not
if [ "$EUID" -ne 0 ]; then
	echo "This sript must run by root" 
	exit 1
fi

# Total Number before opertation
Users_before=$(grep -cE ':[0-9]{4}:' /etc/passwd)
existing_users=()
New_users=0

# Ask how many accounts he wants to add 
read -p "How many accounts you want to add? : " NumAccounts

# Loop to add users 
for ((i=1; i<=$NumAccounts; i++)); do 
	read -p "Enter username for account $i: " username 
# Check if user exists 
	if id "$username" &>/dev/null; then 
		existing_users+=("$username") 
		continue 
	fi 
	
# Set default values or prompt for custom values 
	read -p "Enter home directory for $username (Press Enter for default: /home/$username): " home 
	home=${home:-/home/$username} 
	read -p "Enter shell for $username (Press Enter for default: /bin/bash): " shell    
	shell=${shell:-/bin/bash} 
	
# Create user 
	useradd -d "$home" -s "$shell" "$username" 
	((New_users++)) 
	done
	
# Print existing users 
	if [ ${#existing_users[@]} -gt 0 ]; then
		echo "The following users already exist: ${existing_users[*]}" >&2 
	fi 
	
# Calculate total users after operation 
Users_after=$(grep -cE ':[0-9]{4}:' /etc/passwd)
```

## 6. Asking About adding users to sudoers
```
read -p "Do you want to add any users to sudoers? (yes/no): " add_to_sudoers 
if [ "$add_to_sudoers" = "yes" ]; then 
	read -p "Enter username(s) to add to sudoers (space-separated): " sudo_users 
	for user in $sudo_users; do 
		adduser "$user" sudo 
		echo "$user added to sudoers." 
	done 
fi
```
## Total Code
```
#! /bin/bash
# Check if the user is root or not
if [ "$EUID" -ne 0 ]; then
	echo "This sript must run by root" 
	exit 1
fi

# Total Number before opertation
Users_before=$(grep -cE ':[0-9]{4}:' /etc/passwd)
existing_users=()
New_users=0

# Ask how many accounts he wants to add 
read -p "How many accounts you want to add? : " NumAccounts

# Loop to add users 
for ((i=1; i<=$NumAccounts; i++)); do 
	read -p "Enter username for account $i: " username 
# Check if user exists 
	if id "$username" &>/dev/null; then 
		existing_users+=("$username") 
		continue 
	fi 
# Set default values or prompt for custom values 
	read -p "Enter home directory for $username (Press Enter for default: /home/$username): " home 
	home=${home:-/home/$username} 
	read -p "Enter shell for $username (Press Enter for default: /bin/bash): " shell    
	shell=${shell:-/bin/bash} 
# Create user 
	useradd -d "$home" -s "$shell" "$username" 
	((New_users++)) 
	done
# Print existing users 
	if [ ${#existing_users[@]} -gt 0 ]; then
		echo "The following users already exist: ${existing_users[*]}" >&2 
	fi 
# Calculate total users after operation 
Users_after=$(grep -cE ':[0-9]{4}:' /etc/passwd)
# Print users before & after 
echo "Total users before: $Users_before" 
echo "Total users added: $New_users" 
echo "Total users after: $Users_after"

#check if he wants to add users to sudoers
read -p "Do you want to add any users to sudoers? (yes/no): " add_to_sudoers 
if [ "$add_to_sudoers" = "yes" ]; then 
	read -p "Enter username(s) to add to sudoers (space-separated): " sudo_users 
	if [ -n "$sudo_users" ]; then 
		for user in $sudo_users; do 
			usermod -aG sudo "$user" 
		done 
		echo "Added the following users to sudoers: ${sudo_users[*]}" 
	fi
fi
```
