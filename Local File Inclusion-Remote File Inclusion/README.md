# Local File Inclusion(LFI)/Remote File Inclusion(RFI)

## Objective:
The purpose of this project is to gain practical experience in identifying and exploiting Local File Inclusion (LFI) and Remote File Inclusion (RFI) vulnerabilities within web applications. By setting up Damn Vulnerable Web Application (DVWA) on Virtualbox and using Docker, I aim to create a controlled environment for hands-on exploration. Key tasks and learning objectives include:

**Project Highlights:**

1. Environment Setup:
- Utilize Virtualbox to set up Damn Vulnerable Web Application (DVWA) and Docker on a Kali Linux machine.
- Establish a secure testbed to simulate real-world scenarios for LFI and RFI exploitation.
- Security Level Configuration:
- Configure DVWA security levels to low, medium, and high to simulate different complexities of LFI and RFI vulnerabilities.

2. Local File Inclusion (LFI) Exploration:
- Familiarize myself with the DVWA interface and locate sections related to LFI vulnerabilities.
- Exploit LFI by including local files, starting with the lowest security level and progressing to higher levels.
- Retrieve sensitive information, such as /etc/passwd, and document the steps taken and files accessed at each security level.

3. Remote File Inclusion (RFI) Exploration:
- Repeat the process for RFI vulnerabilities, attempting to include remote files and execute code from a Kali Linux machine.
- Start a Python server on Kali for RFI exploitation, demonstrating the inclusion of remote files and code execution on the target DVWA machine.
- Document the steps taken and files accessed during RFI exploitation at each security level.

4. Issue Resolution:
- Address common issues encountered during exploitation, including enabling the PHP function allow_url_include.
- Provide troubleshooting steps for resolving errors and challenges in the scanning environment.
