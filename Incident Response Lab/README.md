# Incident Response Lab

## Objective: 
The purpose of this lab is to perform a series of cybersecurity exercises focused on Incident Response. I compromised a virtual machine (LazySysAdmin) using a Kali Linux machine and later conducted a digital forensics investigation utilizing Autopsy. This lab aims to provide hands-on experience in both exploiting vulnerabilities and investigating the corresponding indicators of compromise (IoCs).

### IoC 1
- The screenshot reveals an executed command to remove the bash history (rm .bash_history). This action is often indicative of a threat actor attempting to erase their activity logs or conceal the commands executed during their session.

<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Incident%20Response%20Lab/Assets/IRL1.jpg" alt="">
</p>

### IoC 2
- The screenshot displays an entry from the authentication log (/var/auth.log) which highlights a root login via the /dev/tty1 terminal. The use of capital letters in "ROOT LOGIN" indicates that the highly-privileged root account was used for this login. This raises red flags about potential unauthorized access and the associated risks of privilege escalation.

<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Incident%20Response%20Lab/Assets/IRL2.jpg" alt="">
</p>

### IoC 3
- The screenshot demonstrates that the attacker successfully escalated their privileges by assuming the local master browser role within the Samba network. Control over the local master browser could allow the attacker to manipulate network resources, opening the door to additional exploitation or unauthorized access.

<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Incident%20Response%20Lab/Assets/IRL3.jpg" alt="">
</p>
