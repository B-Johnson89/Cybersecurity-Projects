# Mobile Penetration Test

## Objective:

This project focuses on mobile penetration testing, specifically targeting Android devices. The primary goal was to explore vulnerabilities within an Android virtual environment and gain a comprehensive understanding of Android security measures—or lack thereof. The project involved several core objectives, outlined below:

1. **Android Device Penetration:** Using various tools and methodologies to conduct a penetration test on an Android virtual device.
2. **ADB Integration:** Utilizing the Android Debug Bridge (ADB) to establish a connection between a Kali Linux machine and the Android virtual device for deeper inspection and testing.
3. **Information Gathering:** Collecting crucial data about the virtual device, including its brand, model, and name, as well as the list of all installed packages, by executing specific ADB commands.
4. **DIVA App Testing:** Downloading and installing the Damn Insecure and Vulnerable App (DIVA) onto the Android virtual device to examine common vulnerabilities. This involved solving challenges within the app, specifically related to input validation issues.
5. **Documentation and Reporting:** Compiling all steps, methodologies, and findings into a single document, complete with screenshots and explanations, to offer a full view of the penetration testing process and outcomes.

## Walkthrough:

**Enabling USB Debugging:** The assignment began with enabling USB debugging on the Android virtual machine (VM). I navigated to the "Developer Options" in the settings and activated "USB Debugging."

**Network Scanning with Nmap:** Before connecting to the Android VM from my Kali machine, I conducted a network scan using nmap. The command nmap 10.0.2.0/24 revealed the IP addresses of both my Kali VM (10.0.2.6) and the Android VM (10.0.2.9). The Android VM had an open port of 5555 with "freeciv" running on it.

**ADB Connection:** I then established a connection to the Android VM using the command adb connect 10.0.2.9.

**Shell Environment:** Following the successful connection, I initiated a shell environment with the command adb shell.

**Collecting Device Name:** To determine the device name, I entered the command getprop ro.product.device, which returned the value "x86_64."

**Identifying Device Model:** I used the command getprop ro.product.model to find out the device model, which was identified as "VirtualBox."

**Determining Brand Name:** To identify the brand of the Android VM, I executed the command getprop ro.product.brand. The output was "Android-x86."

**Listing Installed Packages:** I listed all installed packages on the device using the command pm list packages -f. The screenshot included in my submission captures a portion of the list.

**DIVA App Installation Prep:** Next, I navigated to the directory where the DIVA APK file was located to prepare for its installation.

**Installing DIVA App:** To install the APK file, I ran the command adb install DivaApplication.apk and received a "Success" message as output.

**Verifying Installation:** To confirm that the DIVA App was installed successfully, I executed adb shell pm list packages. The package "jakhar.aseem.diva" was listed, indicating successful installation.
