# Specialized Scanners CTF

## Objective:
Objective: The purpose of this lab is to provide hands-on experience in using specialized scanning tools within a controlled environment. I engaged in scanning and enumerating web services on a Windows platform, using a combination of Nmap, Dirbuster, Nikto, and other specialized tools. The lab is designed to simulate real-world scenarios where understanding and maneuvering around various cybersecurity challenges is crucial. Key tasks include:

1. **Setting Up the Environment:** Utilizing Kali Linux and Metasploitable 3 Windows Machine to create a testbed for scanning exercises.
2. **Web Services Scanning:** Conducting scans on web services, specifically focusing on identifying and analyzing results on port 8585.
3. **Specialized Scanner Usage:** Researching and employing specialized scanners based on the initial scan results, with a focus on in-depth enumeration.
4. **Problem-Solving:** Addressing common issues encountered during scanning, such as non-responsive ports and dependency errors in tools.

## Walkthrough:
### **NMAP**
1. This screenshot demonstrates the initial step of scanning all ports on the target machine using the command nmap -p- 10.0.2.8. The output shows all open ports, including port 8585, which is highlighted.
<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Specialized%20Scanners/Assets/SS1.jpg" alt="">
</p>

### **Dirbuster**
1. The following step involved running a Dirbuster scan. This screenshot displays the setup, with the target URL set as http://10.0.2.8:8585. The brute-force list, sourced from Dirbuster’s directory (/usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt), was used.
<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Specialized%20Scanners/Assets/SS2.jpg" alt="">
</p>

2. The subsequent screenshot presents the outcomes of the Dirbuster scan. It reveals several directories and files, including those related to a WordPress installation.
  - **Key Findings:**
    - Root Directories and Files:
      - Home Page: /index.php
      - Directories: /cgi-bin/, /icons/, /uploads/
    - WordPress Directories and Files:
      - WordPress Root: /wordpress/
      - WordPress Admin: /wordpress/wp-login.php
      - WordPress Content: /wordpress/wp-content/
      - WordPress Themes: /wordpress/wp-content/themes/
      - WordPress Plugins: /wordpress/wp-content/plugins/
<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Specialized%20Scanners/Assets/SS3.jpg" alt="">
</p>

### **Nikto**
1. This screenshot captures the Nikto scan and its findings on the target machine, executed with the command nikto -h http://10.0.2.8:8585. The -h argument specifies the target host.
  - **Key Findings:**
    - WordPress Vulnerabilities:
      - hello.php plugin reveals the file system path.
      - Server potentially exposes inodes via ETags, detected in the file /wordpress/readme.html.
      - WordPress version disclosed through readme.html and wp-links-opml.php files.
      - WordPress login page at /wordpress/wp-login.php.
      - Browsable WordPress uploads directory at /wordpress/wp-content/uploads/, risking information leakage.
<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Specialized%20Scanners/Assets/SS4.jpg" alt="">
</p>

### **Specialized Scanner (WPScan)**
1. This screenshot illustrates my Google search for a specialized scanner suitable for enumerating port 8585, leading to the selection of the WordPress scanner.
<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Specialized%20Scanners/Assets/SS5.1.jpg" alt="">
</p>

2. I verified the installation of WPScan using the command wpscan –version.
<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Specialized%20Scanners/Assets/SS5.2.jpg" alt="">
</p>

3. A subsequent screenshot shows a WPScan of the target VM’s open port 8585, focusing on the WordPress directory. The scan confidently identified that the Upload Directory at http://10.0.2.8:8585/wordpress/wp-content/uploads/ has listing enabled.
<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Specialized%20Scanners/Assets/SS5.3.jpg" alt="">
</p>

4. This screenshot displays the contents of the upload directory, specifically the wordpress/wp-content/uploads/2016/09 folder, revealing images including the Metasploitable3 flag.
<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Specialized%20Scanners/Assets/SS5.4.jpg" alt="">
</p>

5. The final screenshot is of the Metasploitable3 flag, depicting an image of a man in a hat alongside The RZA, the founder of the Wu-Tang music collective, wearing a red hat on a King of Hearts playing card.
<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Specialized%20Scanners/Assets/SS5.5.jpg" alt="">
</p>
