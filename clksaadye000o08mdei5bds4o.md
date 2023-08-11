---
title: "Day 1 : Bash Scripting Challenge! 🚀"
datePublished: Tue Aug 01 2023 12:37:06 GMT+0000 (Coordinated Universal Time)
cuid: clksaadye000o08mdei5bds4o
slug: day-1-bash-scripting-challenge
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1690893380602/f71ce71e-1259-4ef3-8920-7153923efc33.png
tags: devops, linux-for-beginners, bash-script, trainwithshubham

---

# **🌟 Introduction:**

Bash scripting is a powerful tool that allows DevOps engineers to automate tasks and perform various operations on their systems. Today, we will cover the basics of bash scripting to get you started on this exciting journey. By the end of this challenge, you will have created a single bash script that completes multiple tasks and demonstrates your understanding of the concepts covered.

## **🔱 Task 1: Comments**

In bash scripts, comments play a vital role in making the code more understandable and explaining its functionality. They begin with the `#` symbol. Let's create a bash script with comments explaining what the script does.

```plaintext
#!/bin/bash

# DevOps Engineer: Task 1: Comments
# - In this task, we will use comments to explain the script.
# Output a welcome message to the user
```

## **🔱 Task 2: Echo**

The `echo` command is one of the simplest and most frequently used commands in bash scripting. It is used to display messages on the terminal. Let's create a bash script that uses `echo` to print a message of our choice.

```plaintext
#!/bin/bash

# DevOps Engineer: Task 2: Echo
# - In this task, we use the 'echo' command to print a message.

# Output a welcome message to the user
echo "This is Day 1 of the Bash Scripting Challenge!"
```

## **🔱 Task 3: Variables**

Variables in bash are used to store data and can be referenced by their name. In this task, we will create a bash script that declares variables and assigns values to them.

```plaintext
#!/bin/bash

# DevOps Engineer: Task 3: Variables
# - In this task, we will declare and use variables.

# Declare variables and assign values
user_name="Dushyant Kumar"
user_age=25
user_country="India"

# Output the values of variables
echo "Name: $user_name"
echo "Age: $user_age"
echo "Country: $user_country"
```

## **🔱 Task 4: Using Variables**

Now that we have declared variables, let's use them to perform a simple task. In this task, we will create a bash script that takes two variables (numbers) as input and prints their sum using those variables.

```plaintext
#!/bin/bash

# DevOps Engineer: Task 4: Using Variables
# - In this task, we will use variables to perform a basic calculation.

# Get user input for two numbers
read -p "Enter the first number : " num1
read -p "Enter the second number : " num2

# Calculate the sum of the two numbers
sum=$((num1 + num2))

# Output the result
echo "The sum of $num1 and $num2 is: $sum"
```

## **🔱 Task 5: Using Built-in Variables**

Bash provides several built-in variables that hold useful information. In this task, we will create a bash script that utilizes at least three different built-in variables to display relevant information.

```plaintext
#!/bin/bash

# DevOps Engineer: Task 5: Using Built-in Variables
# - In this task, we will use built-in variables.

# Output the current user
echo "Current user: $USER"

# Output the hostname
echo "Hostname: $HOSTNAME"

# Output the current working directory
echo "Current directory: $PWD"
```

## **🔱 Task 6: Wildcards**

Wildcards are special characters used to perform pattern matching when working with files. In this task, we will create a bash script that utilizes wildcards to list all the files with a specific extension in a directory.

```plaintext
#!/bin/bash

# DevOps Engineer: Task 6: Wildcards
# - In this task, we will use wildcards to list files.

# Define the target directory
target_directory="/home/d_work/k8s_yaml/"

# List all files with a specific extension in the target directory
echo "Files with the '.yaml' extension:"
ls "$target_directory"/*.yaml
```

\\...................................................................................................................................................

The above information is up to my understanding. Suggestions are always welcome. Thanks for reading this article.

#bash #aws #linux #Devops #TrainWithShubham #90daysofdevopsc #happylearning

<mark>Follow for many such contents:</mark>

<mark>LinkedIn</mark>: [**linkedin.com/in/dushyant-kumar-dk**](http://linkedin.com/in/dushyant-kumar-dk)

<mark>Blog</mark>: [**dushyantkumark.hashnode.dev**](http://dushyantkumark.hashnode.dev)