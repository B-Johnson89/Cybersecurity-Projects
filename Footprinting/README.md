# Footprinting

## Objective:
For this project, the focus is on footprinting — a key phase in penetration testing — targeting a Metasploitable3 Linux machine. Utilizing Kali Linux as the operating environment, the project explores both Nmap and RustScan tools for comprehensive port scanning. The project aims to.
1. Conduct a complete port scan of the target machine using Nmap, employing the -A switch to identify service versions on all open ports.
2. Utilize RustScan as an alternative to Nmap for similar port scanning activities and compare its usability.
This project serves as a practical exercise for applying advanced scanning tools in footprinting and offers an in-depth comparison of traditional and emerging tools in the domain.

## Walkthrough

- This screenshot displays the outcome of an initial Nmap scan over the local network, using the command **nmap 10.0.2.0/24**. This scan helped identify the IP address of the Windows Metasploitable VM as 10.0.2.8. I was already aware of my Kali VM's IP address (10.0.2.6), making the ifconfig step unnecessary. The scan also reveals open ports and running services on the network.

<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Footprinting/Assets/FP1.jpg" alt="">
</p>

- The second screenshot features the results from a more comprehensive scan using **nmap -p- -A 10.0.2.8**. This scan aims to identify all open ports and gather advanced information about them, including the versions of each running service and OS detection. Numerous services and their versions are listed, ranging from FTP and SSH to various HTTP servers.

<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Footprinting/Assets/FP2.jpg" alt="">
</p>

- The third screenshot provides an initial glance at RustScan's output, focusing on identifying open ports on the target machine.

<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Footprinting/Assets/FP3.jpg" alt="">
</p>

- This screenshot elaborates on how RustScan automatically delegates detailed scanning tasks to nmap for more comprehensive results. This seamless integration optimizes the scanning process.

<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/Footprinting/Assets/FP4.jpg" alt="">
</p>

- The fifth screenshot highlights the TCP flags associated with the open ports and services, which underscores the reliability of the connection to the target machine. Additionally, an echo of my name appears at the end, adding a personalized touch to the scan results.

<p align="center">
  <img src="" alt="">
</p>
