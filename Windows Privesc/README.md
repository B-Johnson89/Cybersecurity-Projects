# Windows Privilege Escalation

## Objective: 
Windows Privilege Escalation, leveraging tools and techniques to gain unauthorized access to system-level resources on a Windows Server machine within a controlled environment. The lab commences with gaining a limited shell via exploiting Jenkins on port 8484, followed by escalating privileges using Juicy Potato. This project provides hands-on experience in exploiting service vulnerabilities, working with Meterpreter shell, and privilege escalation techniques. The ultimate objective is to attain an NT AUTHORITY\SYSTEM level access, thereby demonstrating the vulnerabilities and the importance of securing Windows systems.

## Walkthrough:

### Part 1

- I initiated a Nmap scan within a specified IP range using the command **nmap 10.0.2.0/25**. Given that my host IP is 10.0.2.6, I deduced that the Windows VM IP is 10.0.2.8 with multiple open ports.
- I noticed that port 8484 wasn’t displayed as open, prompting me to check using the command **nmap -p 8484 -sV 10.0.2.8**. I found it open and identified the running service as **Jetty winstone-2.8**, an HTTP service.
- With this information, I accessed Jenkins by entering the IP address and port number **10.0.2.8:8484** in Firefox.
- I then switched to the terminal and entered **MSFconsole** to search for Jenkins exploits. Following the instructions, I selected **exploit number 6**.
- Setting options for this exploit, I configured the username and password to **vagrant**, defined the rhost as 10.0.2.8 (target IP), set the target URI based on the Firefox URL **http://10.0.2.8:8484/**, defined the srvhost as my host IP (10.0.2.6), and assigned the rport as 8484. Executing the **run** command opened the meterpreter session 1 as NT Authority\local service.
- I verified if the SeImpersonatePrivilege was enabled, and it was.
- Next, I uploaded **JuicyPotato** to the target machine using the meterpreter command **upload /home/kali/Downloads/JuicyPotato.exe**.
- A quick **ls** command confirmed its presence on the machine with **rwx** permissions across all user groups.

### Part 2
