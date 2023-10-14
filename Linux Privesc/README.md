# Linux Privilege Escalation
## **Objective:** Exploit a Linux machine and escalate privileges to gain root access.

- On my Kali VM, I executed **ifconfig** to identify the machine's IP address, which was **10.0.2.6**. I subsequently conducted a scan with command **nmap 10.0.2.0/25** and noted the resulting IP address, **10.0.2.15**, and its open ports, especially port 80. This IP is believed to be that of the Metasploitable VM.

- I accessed the Metasploitable VM's IP **10.0.2.15** via Firefox and navigated to the Drupal directory.

- Launching MSFconsole, I searched for **drupal exploits** and selected exploit number 2, based on its HTTP parameter key, which corresponds to the service running on port 80.

- Upon executing the **use 2** command, I viewed the module options using **show options**. I identified that the RHOSTS (Target IP), RPORT (80), and TARGETURI (URL from Firefox) settings needed configuration.

- Once configured, I initiated the exploit, which led to opening a Meterpreter session. Running **getuid** revealed the username **www-dat**.

- I proceeded to the LinPEAS GitHub page and executed its command on the VM. This initiated LinPeas, and I noted the overlayfs CVE **[CVE-2016-1328] overlayfs**.

- In the Meterpreter session, I searched for **overlayfs modules**, opting for number 1, given its disclosure date matched the year of the identified CVE.

- After executing **use 1**, I set the LHOST (Host IP) options and established the session to number 1.

- Unfortunately, running the exploit didn't generate a session due to PHP's session architecture.

- I reverted to the root directory and identified **payroll_app.php**. Attempting SQL Injection in the username field with **’ OR 1=1#**, I was presented with a list of usernames, full names, and associated salaries.

- Returning to the login page, I inserted **' OR 1=1 UNION SELECT null,null,username,password FROM users#** in the username field. This action revealed another list, which included usernames, passwords, full names, and salaries.

- From this list, I decided to log in as jarjar_binks. As the earlier nmap scan showed port 22 open for SSH, I initiated an SSH session with **jarjar_binks@10.0.2.15**. After inputting the password, I successfully logged in as jarjar_binks.

- In this session, I navigated to the **etc directory** and attempted to view the shadow file using **cat**. Access was denied.

- To escalate privileges, I created an MSFvenom payload. The command **msfvenom -l payloads | grep linux** revealed the desired payload **linux/x86/shell/reverse_tcp**.

- I crafted this payload, configuring the LHOST and LPORT, and saved it as an ELF file named **shells**.

- To transfer the file to the target machine, I utilized scp with the command **scp shells.elf jarjar_binks@10.0.2.15:/home/jarjar_binks**. I verified the transfer using the ls command.

- Back in the MSF console, I searched for a multi-handler and selected number 5, given its generic payload handling capabilities.

- I set the payload options for **linux/x86/shell/reverse_tcp**, including LHOST and LPORT.

- Executing the multi-handler using **run**, I transitioned to the SSH session and ran “./shells.elf”. This action opened shell session 2 in msfconsole, confirming my login as jarjar_binks via the **whoami** command.

- I returned to the MSF console, repeated the overlayfs search, and used option 1 again. Setting the session to number 2 and running the exploit opened session 3, wherein I had root access, confirmed by the **whoami** command.

- Navigating to the etc directory and executing cat on the shadow file, I finally gained access.
