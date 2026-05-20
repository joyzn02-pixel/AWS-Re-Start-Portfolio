# Lab 03 - Linux Command Line

**Programme:** Praesignis AWS re/Start **Date completed:** 20 May 2026 **Lab topic:** Linux CLI - System information commands and bash history

---

## 📝 What This Lab Covered

This lab built on the previous SSH connection skills to explore essential Linux command line tools. The focus was on running system information commands to understand the current environment, and using bash history features to improve workflow efficiency by reusing and searching previous commands.

Key concepts practised:

- Using Tab autocomplete to finish commands faster
- Running `whoami` to identify the current user
- Using `hostname -s` to display the shortened system hostname
- Using `uptime -p` to check how long the system has been running
- Using `who -H -a` to view logged-in users and session details
- Displaying date and time across different time zones using `TZ=`
- Viewing the Julian calendar with `cal -j`
- Viewing alternate calendar layouts with `cal -s` and `cal -m`
- Using `id ec2-user` to view user ID and group memberships
- Viewing full command history with `history`
- Searching previous commands using `Ctrl+R` reverse search
- Rerunning the last command using `!!`

---

## 📸 Screenshots and Explanations

### Screenshot 01 - SSH Connection Successful

A fresh PEM key was downloaded for this lab session. The terminal shows a successful SSH connection to the EC2 instance, with the Amazon Linux 2 welcome banner confirming access. The prompt shows `[ec2-user@ip-10-0-10-135 ~]$`.

![SSH Connection Successful](screenshot-01-ssh-connected.png)

---

### Screenshot 02 - System Information Commands

The following commands were run to gather information about the current system and session:

- `whoami` returned `ec2-user`, confirming the current logged-in user
- `hostname -s` returned `ip-10-0-10-135`, the shortened hostname of the instance
- `uptime -p` showed the system had been running for 12 minutes
- `who -H -a` displayed active session details including login time, PID, and the connecting IP address
- `TZ=America/New_York date` returned `Wed May 20 02:22:10 EDT 2026`
- `TZ=America/Los_Angeles date` returned `Tue May 19 23:22:25 PDT 2026`
- `cal -j` displayed May 2026 in Julian format, with today highlighted as day **140**

![System Information Commands](screenshot-02-system-commands.png)

---

### Screenshot 03 - Calendar Views

- `cal -j` displayed the Julian calendar for May 2026, where dates run consecutively through the year rather than restarting each month
- `cal -s` displayed the standard Sunday-first calendar view
- `cal -m` displayed the Monday-first calendar view

Today (20 May 2026) was highlighted in all three views.

![Calendar Views](screenshot-03-calendar-views.png)

---

### Screenshot 04 - History and Command Reuse

- `id ec2-user` displayed the user ID, group ID, and all groups the user belongs to including Sales, HR, Finance, Shipping, Managers, and CEO
- `history` listed all 11 commands run during the session in order
- `TZ=America/Los_Angeles date` was rerun after using `Ctrl+R` reverse search
- `!!` was used to rerun the last command, demonstrating how to quickly repeat previous commands without retyping them

![History and Command Reuse](screenshot-04-history-commands.png)

---

### Screenshot 05 - Submission Report

The lab was submitted successfully before ending the session.

![Submission Report](screenshot-05-submission-report.png)
