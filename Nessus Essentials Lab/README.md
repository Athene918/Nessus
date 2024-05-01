## Nessus Essentials Lab: Vulnerability Management

### Description
Today’s lab is focused on Vulnerability Management. We will build a Vulnerability Management Lab by installing Nessus Essentials on our host machine and creating a virtual environment using VMWare Workstation 17. This involves downloading a free copy of the Windows 10 operating system and running it inside a virtual machine (VM). Additionally, we'll install some old, deprecated software on the Windows OS. The objective is to conduct vulnerability scans against the virtual machine to discover any vulnerabilities present. Subsequently, we will remediate one or two of those vulnerabilities to observe real-time outcomes.

#### Scan Procedure:
1. **Non-Credentialed Scan (Pre-Update):**
    - Conduct a vulnerability scan without credentials before applying any updates to the target machine.

2. **Credentialed Scan (Pre-Update):**
    - Perform a vulnerability scan with credentials before applying any updates to the target machine.

3. **Credentialed Scan (Post-Update):**
    - Execute a vulnerability scan with credentials after applying updates to the target VM.

At the conclusion of this lab, we will compare the results of the three scans to analyze the effectiveness of the vulnerability management process.

## Learning Objectives

1. **Provisioning and Deprovisioning Virtual Environments:**
    - Set up and remove virtual environments within VMware for Windows 10.

2. **Initial Vulnerability Scan (Non-Credentialed):**
    - Conduct an initial vulnerability scan without credentials against the VM and observe the results.

3. **Credentialed Vulnerability Scan with Deprecated Software:**
    - Run a credentialed vulnerability scan after adding deprecated software to the VM.

4. **Analysis and Remediation:**
    - Analyze scan results, perform remediation of identified issues, and run a final scan to verify successful remediation.

## Technologies and Protocols

- VMware Workstation 17 Player
- Nessus Essentials
- Windows ISO + Firefox 3.6.12

**NOTE:** This lab will be conducted on a Windows machine.

## Resource Links

- [VMware Workstation Player](https://www.vmware.com/products/workstation-player/workstation-player-evaluation.html)
- [Windows 10 ISO](https://www.microsoft.com/en-us/software-download/windows10)
- [Nessus Essentials](https://www.tenable.com/products/nessus/nessus-essentials)
- [Deprecated Firefox Version for VM Install](https://ftp.mozilla.org/pub/firefox/releases/3.6.12/win32/en-US/)


## Overview:

![Lab](https://miro.medium.com/v2/resize:fit:720/format:webp/0*QJljnd-LgZLWOYBT.png)

## Get Set Up: Download VMware Workstation 17 Player

- Go to the [VMware Workstation Player website](link_to_vmware_player).
- Find the download section and select the appropriate version for your operating system.
- Follow the on-screen instructions to complete the download and installation process.

## Continue Set Up: Download Windows 10 ISO File

- Go to the [Microsoft Windows 10 download page](link_to_windows10_download).
- Scroll down to the media creation tool section and click on "Download Now."
- Accept the software license terms and agree to the Windows 10 setup.
- Follow the prompts to create installation media and choose the ISO file option.

![Windows](https://miro.medium.com/v2/resize:fit:720/format:webp/0*bU62yTrkSG8c9E-2.png)

## Part 1: Download and Install Nessus Essentials

1. **Register for an account:**
   - Go to the [Nessus Essentials website](https://www.tenable.com/products/nessus/nessus-essentials).
   - Sign up for an account by following the instructions.

2. **Receive an activation code in your email:**
   - After completing the registration, you will receive an activation code in your email.

3. **Download Nessus:**
   - On the Nessus website, download version 10.6.2 for the Windows platform (x86_64).

4. **Open and install Nessus:**
   - After downloading, open the Nessus installation file.
   - Follow the instructions to install the software.
   - A window should pop up with a localhost URL.

5. **Copy/paste the URL for future use:**
   - Copy the displayed URL for future use. You will need it to access Nessus.

![Nessus](https://miro.medium.com/v2/resize:fit:720/format:webp/0*1yxoK5zerOG5DHqP.PNG)

## Part 2: Initialize Nessus Installation

1. **Connect via SSL on web page:**
   - Access Nessus using the localhost URL provided during installation.
   - Ensure to connect via SSL by clicking on the appropriate option on the web page.

2. **Click Advance on warning page:**
   - If a warning page appears, click on "Advance."
   - Then click on "Continue to localhost" to proceed to the Nessus Essentials page.

3. **Skip activation code retrieval:**
   - If prompted to "Get an activation code," click on "Skip" as you already have your activation code from the email.

4. **Paste activation code from email:**
   - Paste the activation code you received in your email into the provided field.
   - Click "Continue" to proceed.

5. **Create a username and password:**
   - Create a username and password for your Nessus account. Make sure to remember these for future use.

6. **Click submit:**
   - After creating your account credentials, click "Submit" to proceed.
   - Wait for the download to complete.

![Nessus](https://miro.medium.com/v2/resize:fit:720/format:webp/0*5USy_uDsqZVd5Hgs.png)

**NOTE:** Copy and save the local URL for Nessus so it is easy to access in the future.
- **Nessus URL:** [https://localhost:8834/#](https://localhost:8834/#)

## Part 3: Setup Target Virtual Machine

1. **Open VMware Workstation:**
   - Launch VMware Workstation on your computer.

2. **Create a New Virtual Machine:**
   - Click on "Player" > "File" > "New Virtual Machine" in the menu bar.

3. **Select Windows 10 ISO:**
   - For the "Installer disc image file (ISO)," browse and select your Windows 10 ISO file.

4. **Customize Virtual Machine Settings:**
   - Under "Customize," set the following:
      - Memory: 4GB (4096 MB)
      - Network Adapter: Bridged

5. **Finish Configuration:**
   - Click "Finish" to complete the setup.

6. **Install Windows:**
   - Open the newly created virtual machine and follow the on-screen instructions to install Windows.
   - Remember the username and password you create during the account setup.

![VMWare](https://miro.medium.com/v2/resize:fit:720/format:webp/0*2sH6ZbPL52lJ-rke.PNG)

## Part 4: Configure Target Virtual Machine Firewall

1. **Get Target VM IP Address:**
   - On the target VM, open `cmd.exe`.
   - Run the command `ipconfig` to retrieve the IP address of the VM.

2. **Ping Target VM from Host Machine:**
   - On the host machine, open `cmd.exe`.
   - Run the command `ping <target_VM_IP_address> -t` to continuously ping the target VM.
   - Replace `<target_VM_IP_address>` with the IP address obtained from step 1.

3. **Observe Firewall Settings:**
   - If the ping requests result in "Request Timed-Out," it indicates that the firewall settings on the target VM are preventing scanning.

![Windows](https://miro.medium.com/v2/resize:fit:720/format:webp/0*fYPku0pBptjF2X2B.PNG)

**NOTE:** We must change firewall settings on the Target VM in order to scan it and run Nessus against it.

1. **Turn Off Firewall Profiles:**
   - On the Target VM, go to the Search Bar and type `wf.msc`.
   - In the Windows Firewall with Advanced Security window, turn off the Domain, Private, and Public Profiles.

2. **Verify Connection:**
   - Immediately after turning off the firewall profiles, verify the connection by pinging the target VM again.
   - If the ping returns a result, it indicates that the firewall settings have been successfully modified, and we can proceed with the scanning process.

![Windows](https://miro.medium.com/v2/resize:fit:720/format:webp/0*8Zl3fN4aW1G0YQtt.PNG)

## Part 5: Run Basic Network Scan (Non-Credentialed)

1. **Access Nessus Dashboard:**
   - Navigate to "My Scans" in the Nessus dashboard.

2. **Start New Scan:**
   - Click on "New Scan" to create a new scan.

3. **Select Basic Network Scan:**
   - Choose "Basic Network Scan" from the available options.

4. **Configure Scan Details:**
   - Set the following details for the scan:
      - **Name:** Windows 10 Single Host
      - **Target:** 192.168.1.132 (or the IP address of your target VM)

5. **Run the Scan:**
   - Once the scan details are configured, hit the "Play" button to run the scan.

![Nessus](https://miro.medium.com/v2/resize:fit:720/format:webp/0*cuz8-Hr0DmMKwMS3.PNG)

**NOTE:** Nessus is highly customizable. You can run Scheduled Scans, Change Port Settings, and Create Reports as needed.

- Basic Scan Results (Non-Credentialed) show minimal (16) vulnerabilities.

- Click into each vulnerability for a Description and recommended Solutions.

![Nessus](https://miro.medium.com/v2/resize:fit:720/format:webp/0*SZSj8msYCiWPDeej.PNG)

## Part 6: Re-Configure Target Virtual Machine

1. **Enable Remote Registry:**
   - Open `services.msc`.
   - Find "Remote Registry" in the list of services, and open its properties.
   - Set the startup type to "Automatic" and click "Start" to enable it.

2. **Enable File and Printer Sharing:**
   - Go to "Advanced sharing settings."
   - Turn on file and printer sharing for Private, Guest, and All Networks.

3. **Disable User Account Control (UAC):**
   - Open "User Account Control Settings."
   - Set the UAC level to the lowest setting.

4. **Registry Edit Hack (Add Local Account Token):**
   - Open `regedit.msc`.
   - Refer to the Nessus article for specifications on adding the Local Account Token.

5. **Restart Target Virtual Machine:**
   - After making the above changes, restart the target virtual machine to apply the settings.

![Nessus](https://miro.medium.com/v2/resize:fit:720/format:webp/0*0FIBEIjH040WLWSR.PNG)

## Part 7: Run Second Scan (Credentialed)

1. **Configure Credentials in Nessus:**
   - In Nessus, select the checkbox next to the target VM.
   - Click on "More" and then "Configure."
   - Navigate to the "Credentials" tab.

2. **Enter Windows Credentials:**
   - Under Windows, enter the following credentials:
      - **Username:** randall
      - **Password:** ######## (enter the password)

3. **Find Username (if needed):**
   - If you're unsure of the username, open `cmd.exe` and type `whoami` to find the current username.

4. **Save and Run Scan:**
   - After entering the credentials, save the settings.
   - Run the scan to perform a credentialed vulnerability assessment.

![Nessus](https://miro.medium.com/v2/resize:fit:720/format:webp/0*x7moO-W9NjNX9NNK.PNG)

**NOTE:** Second Scan Results (Credentialed) show a significant increase (40) in vulnerabilities.

- Credentials gave us access to File System, Registry, and Running Services (safeguard your credentials).

- This highlights the importance of running a Credentialed Scan and the valuable information it provides.

## Part 8: Run Third Scan (Deprecated Software — Firefox)

1. **Install Deprecated Firefox Version 3.6.12 on Target Virtual Machine:**
   - Download the deprecated Firefox version 3.6.12 installer.
   - Install Firefox 3.6.12 on the target virtual machine.

2. **Back to Nessus:**
   - Once Firefox 3.6.12 is installed on the target VM, return to Nessus.

3. **Run Scan:**
   - In Nessus, initiate a new scan targeting the target VM with Firefox 3.6.12 installed.
![Nessus](https://miro.medium.com/v2/resize:fit:720/format:webp/0*F_0TgVG0KzelJriE.PNG)

**NOTE:** Third Scan Results (Credentialed) with Deprecated Firefox Install show an even greater increase (45) in vulnerabilities.

- The increase comes in the form of Critical Vulnerabilities, up 25%, and High Vulnerabilities, up 40%.

![Nessus](https://miro.medium.com/v2/resize:fit:720/format:webp/0*db50A4rqgxNNzNYi.PNG)

**NOTE:** The majority of recommended Remediations involve simple Updates to OS and Software.

## Part 9: Remediation through Updates and Patching

1. **Uninstall Deprecated Firefox:**
   - On the target virtual machine, search for and run `appwiz.cpl`.
   - Locate Firefox in the list of installed programs and uninstall it.

2. **Install Windows Updates:**
   - Search for "Windows Update" on the target VM and select it.
   - Install all available updates.
   - Restart the virtual machine after installing updates.

3. **Install Any New Updates:**
   - After restarting, search for "Windows Updates" again.
   - Install any new updates that may be available.
   - Restart the virtual machine if prompted.

![Image](https://miro.medium.com/v2/resize:fit:720/format:webp/0*i8INeMoIT-wuIwDT.PNG)

## Part 10: Run Final Scan

1. **Return to Nessus:**
   - Open Nessus on your machine.

2. **Initiate Final Scan:**
   - Start a new scan in Nessus, targeting the previously scanned virtual machine.

3. **Run the Scan:**
   - Configure the scan settings as needed.
   - Start the scan to assess the effectiveness of the implemented general remediations.

![Nessus](https://miro.medium.com/v2/resize:fit:720/format:webp/0*zFavrZX8d3VxvQ_f.PNG)

## Results and Takeaways

### Scan 1: Target Re-configured (Credentialed) Results
- **Risk Rating Percentage:**
   - Critical: 2.00%
   - High: 2.00%
   - Medium: 2.00%
   - Low: 0.00%
   - Info: 95.00%
   - Total: 100.00%

Non-credentialed scans are not as useful as credentialed scans when trying to get an accurate view of vulnerabilities that exist on a device or network because they lack proper access. Non-credentialed scans cannot see vulnerabilities that may exist on parts of a device or network that are off limits without proper authentication. As a result, non-credentialed scans produce far fewer results than credentialed scans. That makes credentials very important to a threat actor because of the access it gives them. Run credentialed scans when possible.

### Scan 2: Firefox (Credentialed) Results
- **Risk Rating Percentage:**
   - Critical: 27.00%
   - High: 26.00%
   - Medium: 6.00%
   - Low: 0.00%
   - Info: 40.00%
   - Total: 100.00%

The second credentialed scan was on a target running third-party software that was outdated. Even if the target VM was running an up-to-date OS, the third-party software would still leave it open to attacks. The more third-party software you have installed, the larger the attack surface you create. Zero trust and system hardening are ways to minimize your attack surface so that you minimize your vulnerability count.

### Scan 3: Remediated (Credentialed) Results
- **Risk Rating Percentage:**
   - Critical: 2.00%
   - High: 2.00%
   - Medium: 2.00%
   - Low: 0.00%
   - Info: 94.00%
   - Total: 100.00%

The third credentialed scan after remediations were implemented shows far fewer vulnerabilities than the previous credentialed scans run before updates were applied. These results demonstrate the importance of scheduling regular vulnerability scans against networks and devices. They also show that keeping systems up to date with the latest patches can drastically reduce the number of vulnerabilities an attacker could exploit.

