# Linux
# ENVIRONMENT VARIABLES

When assigning variables in Bash (and Zsh, which we're using in this lab), there should be no spaces around the equals sign (=). my_var = "Hello, Linux" or my_var= "Hello, Linux" will cause an error.

my_var="Hello, Linux"

To view the value of the variable, we use the echo command with a $ before the variable name. The $ tells the shell to substitute the value of the variable:
echo $my_var
echo "The value of my_var is:$my_var" //output:the value of my_var is:Hello, Linux

Environment variables are variables that are available to any child process of the shell. This means they can be accessed by scripts and programs run from that shell.

To view all current environment variables, use the env command.

One of the most important environment variables is PATH.
The PATH variable lists directories where the system looks for executable programs. Each directory is separated by a colon (:).

Now, let's create our own environment variable. We use the export command to create an environment variable:
export MY_ENV_VAR="This is an environment variable"
The export command makes the variable available to child processes. This is the key difference between shell variables and environment variables.

To illustrate the difference, let's create a shell script that tries to access both a regular shell variable and an environment variable:

echo '#!/bin/bash
echo "Shell variable: $my_var"
echo "Environment variable: $MY_ENV_VAR"' > test_vars.sh
 Explain Code
Make the script executable:

chmod +x test_vars.sh
Now run the script:

./test_vars.sh
You should see that the environment variable (MY_ENV_VAR) is accessible, while the shell variable (my_var) is not. This is because my_var was not exported, so child processes (like the script) don't know about it.

To verify that MY_ENV_VAR is now an environment variable, we can use the env command again, but this time we'll filter the output using grep:

env | grep MY_ENV_VAR
 Explain Code
You should see your new variable in the output.

Environment variables and shell variables each have their own scope. When you export a variable (e.g., export MY_ENV_VAR="something"), it becomes available to any subprocess started from that shell (for example, a shell script run by that same shell). However, if you open a completely separate shell session, it does not inherit the variables from your current shell unless you specifically set them in a startup file (like .zshrc or .bashrc).

In other words:

A regular shell variable is visible only within the current session.
An exported variable is available to child processes launched from that session.
A variable set in a shell startup file (like .zshrc) is applied to all new sessions of that shell.
You cannot directly read another user’s or another shell’s variables because each process maintains its own environment. If you start a new shell, it gets a copy of the parent’s exported variables but not variables set only in the original shell without export.
