# Windows Buffer Overflow

## Objective:
This project is centered on understanding and executing a Windows buffer overflow. By targeting a specific Windows virtual machine, the project aimed to shed light on the intricacies of buffer overflow vulnerabilities in a Windows environment, emphasizing the steps and tools necessary to exploit such flaws. The key objectives of the project are detailed below:
- **Manual Buffer Overflow:** Engaging in a step-by-step process to perform a buffer overflow against a Windows target, understanding the specific conditions and elements that lead to successful exploitation.
- **Immunity Debugger Integration:** Leveraging the Immunity Debugger to trace and understand the buffer overflow process in real time. This involved attaching specific processes to the debugger and observing program behavior during exploitation attempts.
- **Character Testing and EIP Control:** Using a fuzzer script to determine the exact point of EIP overwrite, followed by a systematic approach to identifying and removing bad characters to ensure the crafted payload's effectiveness.
- **Payload Crafting and Exploitation:** Utilizing MSFvenom to generate a specific payload, followed by setting breakpoints and adjusting scripts to gain control over the program's execution. Successfully exploiting the vulnerability led to obtaining a reverse shell on the target machine.

## Walkthrough:

