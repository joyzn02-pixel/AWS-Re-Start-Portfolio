# Lab 02 - Introduction to Amazon Linux AMI

**Programme:** Praesignis AWS re/Start **Date completed:** 20 May 2026 **Lab topic:** Linux CLI fundamentals - SSH access and navigating the Linux man pages

---

## 📝 What This Lab Covered

This lab introduced the fundamentals of connecting to and navigating an Amazon Linux EC2 instance using the command line. It focused on two core skills: using SSH to securely access a remote server, and using the Linux manual (man) pages to understand how commands work.

Key concepts practised:

- Downloading a PEM key file and setting correct permissions using `chmod 400`
- Using SSH from a Mac terminal to connect to an Amazon Linux EC2 instance
- Understanding the structure of an SSH command (`ssh -i keyfile.pem ec2-user@ip`)
- Navigating a remote Linux environment via the command line
- Using the `man` command to access built-in Linux documentation
- Identifying key man page sections: NAME, SYNOPSIS, DESCRIPTION, OPTIONS, EXAMPLES, and SEE ALSO
- Understanding Linux manual section numbers (1–9) and what each category covers

---

## 📸 Screenshots and Explanations

### Screenshot 01 - SSH Connection Successful

The terminal shows a successful SSH connection to the EC2 instance using the downloaded PEM key. The Amazon Linux welcome banner confirms the connection was established and the instance is accessible. The prompt changed to `[ec2-user@ip-10-0-10-50 ~]$` indicating we are now operating inside the remote server.

---

### Screenshot 02 - man man Command Output (Top of Page)

The `man man` command was entered in the terminal. This opens the manual page for the `man` command itself. The top of the page shows the **NAME** and **SYNOPSIS** sections, which describe what the command is and the syntax for using it.

---

### Screenshot 03 - DESCRIPTION Section with Section Numbers

Scrolling down reveals the **DESCRIPTION** header. This section explains that the manual is divided into numbered sections:

- **1** - Executable programs or shell commands
- **2** - System calls
- **3** - Library calls
- **4** - Special files
- **5** - File formats and conventions
- **6** - Games
- **7** - Miscellaneous
- **8** - System administration commands
- **9** - Kernel routines

This helps users understand where to look depending on what type of command or function they are researching.

---

### Screenshot 04 - Submission Report

The lab submission report confirms successful completion, executed on 20 May 2026.
