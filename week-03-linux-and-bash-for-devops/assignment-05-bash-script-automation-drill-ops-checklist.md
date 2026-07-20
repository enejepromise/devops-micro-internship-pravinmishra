# Assignment 5 — Bash Script Automation Drill (OPS Checklist)

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will practice Bash scripting by building a series of small automation scripts covering environment setup, variables, arrays, loops, file conditionals, if-else logic, and functions. These scripts form the foundation of real-world Linux automation used in DevOps, cloud, and production support environments.

---

# Task 1 — Bash Environment & Workspace Setup

## Goal

Verify that Bash is available on your system and create a clean workspace for this assignment.

### Evidence

#### Screenshot 1 — Output of `echo $SHELL` and `bash --version`

![alt text](<task 5 1.PNG>)
---

#### Screenshot 2 — Output of `pwd` and `ls -lah` showing the scripts directory

![alt text](<task 5 2.PNG>)
---

### Notes

Answer the following in your own words:

**1. What is Bash?**

Bash is a command-line interpreter that reads and understands Bash commands entered by the user, communicates those commands to the Linux operating system, and then displays the operating system's response back to the user.

---

**2. What is the difference between shell and Bash?**
A shell is a command-line interpreter that provides an interface between the user and the operating system. It interprets user commands, sends them to the operating system for execution, and displays the results.
while 
Bash is one specific type ofshell.
It performs all the jobs of a shell, but it also includes many powerful features for scripting and automation.

---

**3.It is important to confirm the Bash version before writing scripts because different Bash versions support different features and syntax. A script written for a newer version of Bash may not work on an older version, leading to errors or unexpected behavior. By checking the Bash version, developers can ensure their scripts are compatible with the target systems and avoid deployment issues.


---

# Task 2 — Your First Bash Script

## Goal

Create your first Bash script, make it executable, and run it from the terminal.

### Evidence

#### Screenshot 1 — Content of `first-script.sh`

![alt text](<task 5 3.PNG>)

---

#### Screenshot 2 — Output of `./first-script.sh`

![alt text](<task 5 4.PNG>)

---

#### Screenshot 3 — Output of `ls -l first-script.sh` showing executable permission

![alt text](<task 5 5.PNG>)

---

### Notes

Answer the following in your own words:

**1. What is the purpose of `#!/bin/bash`?**

#!/bin/bash is called the shebang. It tells the operating system to execute the script using the Bash interpreter located at /bin/bash

---

**2. Why do we use `chmod +x` before running a script?**
chmod +x is used to give a script execute permission. Without execute permission, Linux will not allow the script to be run directly.

---

**3. What is the difference between running a script using `./script.sh` and `bash script.sh`?**
./script.sh executes the script directly and requires execute permission. bash script.sh starts the Bash interpreter and tells it to read the script, so execute permission is not required.

---

# Task 3 — Variables: User Information Script

## Goal

Use variables to store and display user-related information.

### Evidence

#### Screenshot 1 — Content of `user-info.sh`

![alt text](<task 5 6.PNG>)

---

#### Screenshot 2 — Output of `./user-info.sh`

![alt text](<task 5 7.PNG>)

---

### Notes

Answer the following in your own words:

**1. What is a variable in Bash?**

A variable in Bash is a named container used to store data or values that can be accessed and reused throughout a script.
---

**2. Why should we avoid spaces around the `=` sign when creating variables?**

Spaces are not allowed around the = sign because Bash interprets spaces as separators between commands and arguments. Using spaces causes Bash to treat the variable name as a command instead of a variable assignment.
---

**3. How do you access the value stored inside a Bash variable?**

You access the value of a Bash variable by placing a dollar sign ($) before the variable name, for example: echo $name.
---

# Task 4 — Arrays & Loops: Tools Checklist Script

## Goal

Use arrays and loops to print a checklist of tools used in Bash scripting.

### Evidence

#### Screenshot 1 — Content of `tools-checklist.sh`

![alt text](<task 5 8.PNG>)
---

#### Screenshot 2 — Output of `./tools-checklist.sh`

![alt text](<task 5 9.PNG>)

---

### Notes

Answer the following in your own words:

**1. What is an array in Bash?**

An array in Bash is a variable that can store multiple values under a single variable name.
---

**2. Why are arrays useful in scripts?**

Arrays are useful because they allow multiple related values to be stored in a single variable, making scripts shorter, easier to manage, and ideal for automation.
---

**3. What does `"${tools[@]}"` mean?**

${tools[@]} represents all the elements stored in the tools array. It is commonly used to loop through or display every item in the array.
---

**4. What is the purpose of the `for` loop in this script?**

The purpose of the for loop is to repeat a block of commands for each item in a list or array. In this script, it goes through every element in the tools array one by one and executes the commands inside the loop for each element
---

# Task 5 — Loops: Number Counter Script

## Goal

Use loops to repeat a task multiple times.

### Evidence

#### Screenshot 1 — Content of `counter.sh`

![alt text](<task 5 10.PNG>)

---

#### Screenshot 2 — Output of `./counter.sh`

![alt text](<task 5 11.PNG>)

---

### Notes

Answer the following in your own words:

**1. What is a loop?**

A loop is a programming structure that repeatedly executes a block of code until a specified condition is met or all items in a list have been processed.
---

**2. Why do we use loops in Bash scripting?**

We use loops in Bash scripting to automate repetitive tasks. Loops reduce the amount of code we write, save time, and make scripts easier to read and maintain.
---

**3. How many times did the loop run in your script?**

The loop ran 5 times

---

**4. What would you change if you wanted the loop to run 10 times?**

if i wanted to the loop run 10 times, i will change the for number in 1 2 3 4 5 to a list {1..10}


---

# Task 6 — Files & Conditionals: File Validation Script

## Goal

Use file checks and conditionals to verify whether files and directories exist.

### Evidence

#### Screenshot 1 — Output of `ls -lah ../test-folder`

Add your screenshot here.

---

#### Screenshot 2 — Content of `file-check.sh`

Add your screenshot here.

---

#### Screenshot 3 — Output of `./file-check.sh`

Add your screenshot here.

---

### Notes

Answer the following in your own words:

**1. What does `-d` check in Bash?**

Add your answer here.

---

**2. What does `-f` check in Bash?**

Add your answer here.

---

**3. Why should file and directory paths be stored in variables?**

Add your answer here.

---

**4. What happens if the file does not exist?**

Add your answer here.

---

# Task 7 — Conditionals: Pass or Retry Script

## Goal

Use if-else conditionals to make decisions based on a variable value.

### Evidence

#### Screenshot 1 — Content of `score-check.sh` with `score=85`

Add your screenshot here.

---

#### Screenshot 2 — Output showing `Result: Pass`

Add your screenshot here.

---

#### Screenshot 3 — Content of `score-check.sh` with `score=55`

Add your screenshot here.

---

#### Screenshot 4 — Output showing `Result: Retry`

Add your screenshot here.

---

### Notes

Answer the following in your own words:

**1. What is the purpose of if-else in Bash?**

Add your answer here.

---

**2. What does `-ge` mean?**

Add your answer here.

---

**3. Why should conditions be tested with different values?**

Add your answer here.

---

**4. How can conditionals help in automation scripts?**

Add your answer here.

---

# Task 8 — Functions: Final Bash Automation Script

## Goal

Create a final Bash script using functions to organize reusable code.

### Evidence

#### Screenshot 1 — Content of `final-automation.sh`

Add your screenshot here.

---

#### Screenshot 2 — Output of `./final-automation.sh`

Add your screenshot here.

---

#### Screenshot 3 — Output of `ls -lah` showing all created scripts

Add your screenshot here.

---

### Notes

Answer the following in your own words:

**1. What is a function in Bash?**

Add your answer here.

---

**2. Why are functions useful in scripts?**

Add your answer here.

---

**3. Which functions did you create in this script?**

Add your answer here.

---

**4. How does this final script combine variables, arrays, loops, conditionals, files, and functions?**

Add your answer here.

---

# LinkedIn Post (Required)

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

`__________________________`

---

#### Screenshot — Published LinkedIn post

Add your screenshot here.

---

# Submission Instructions

- Add all required screenshots in your submission
- Full name must be visible in required screenshots
- All script files must be created and run successfully
- Required notes must be answered clearly for every task
- Do not expose sensitive information (keys, passwords, credentials)

---

# Completion Checklist

- [ ] Task 1: Environment setup verified, workspace created (Screenshots 1–2, Notes answered)
- [ ] Task 2: First script created, executed, permissions verified (Screenshots 1–3, Notes answered)
- [ ] Task 3: Variables script created and run (Screenshots 1–2, Notes answered)
- [ ] Task 4: Arrays and loops script created and run (Screenshots 1–2, Notes answered)
- [ ] Task 5: Counter loop script created and run (Screenshots 1–2, Notes answered)
- [ ] Task 6: File validation script created and run (Screenshots 1–3, Notes answered)
- [ ] Task 7: Pass/Retry conditional script tested with both values (Screenshots 1–4, Notes answered)
- [ ] Task 8: Final automation script created and run (Screenshots 1–3, Notes answered)
- [ ] All scripts run without errors
- [ ] Full Name visible in all required screenshots
- [ ] LinkedIn post published and URL submitted
- [ ] No sensitive data exposed

---

## 📌 About DMI & CloudAdvisory

DevOps Micro Internship (DMI) is a project-based DevOps program run by Pravin Mishra (The CloudAdvisory) focused on real-world execution, systems thinking, and career readiness.

It helps learners build strong DevOps foundations with hands-on experience.

---

## 📌 Resources

- 🌐 DMI Official Website: https://pravinmishra.com/dmi  
- 🎓 DevOps for Beginners (Udemy): https://www.udemy.com/course/devops-for-beginners-docker-k8s-cloud-cicd-4-projects/  
- 🎓 Agentic AI DevOps with Claude Code: https://www.udemy.com/course/ultimate-agentic-ai-devops-with-claude-code/  
- 🎓 DevOps with Claude Code: Terraform, EKS, ArgoCD & Helm: https://www.udemy.com/course/devops-with-claude-code-terraform-eks-argocd-helm/  
- ▶️ YouTube Playlist: https://www.youtube.com/playlist?list=PLFeSNDtI4Cho  
- 🔗 Pravin Mishra (LinkedIn): https://www.linkedin.com/in/pravin-mishra-aws-trainer/  
- 🏢 CloudAdvisory (LinkedIn): https://www.linkedin.com/company/thecloudadvisory/

---

*This submission is part of DevOps Micro Internship (DMI) Cohort 3 — Agentic AI Track.*