# PCAP_Lab_2

## Objective

Conduct PCAP analysis via Wireshark and provide a report on attack vectors used and various IOCs associated with malware infection.
This lab focuses specifically on an AsycRAT and XWorm infection.

### Skills Learned

- PCAP Analysis
- Detailed understanding of web traffic components as they relate to the OSI model
- Improved overall analytical skills
- Better understanding of encryption protocols and PKI framework

  
### Tools Used

- Wireshark
- NMAP

### Steps

Made a few changes to my setup this time around. I used my Kali Linux VM this time, to prevent inadvertent infection of my Windows laptop when downloading malicious files form the PCAP.
###
I filter for HTTP events and immediately notice suspicious activity
###
![2024-04-11 12_06_54-Kali Linux on GENIE - Virtual Machine Connection](https://github.com/Benrosan/PCAP-Lab-2/assets/160042310/b17c44cb-2bae-4176-8f68-7bba64bd52f2)
###
The host check for permitted HTTP options and the server returns the following (obtained by following TPC stream).
###
![2024-04-11 12_10_59-Kali Linux on GENIE - Virtual Machine Connection](https://github.com/Benrosan/PCAP-Lab-2/assets/160042310/ce2020a2-c5c6-46da-9762-a1f5344342d3)
###
The host then starts looking for a specific batch file: `file.bat` via PROPFIND method. 
###
Once the file is found, the host downloads the file. Following the TCP Stream on the GET method shows the Python code that's contained in `file.bat` and executed on the host:
###
![2024-04-11 12_29_55-Kali Linux on GENIE - Virtual Machine Connection](https://github.com/Benrosan/PCAP-Lab-2/assets/160042310/3576d8da-7cd5-4743-9fc3-dbd44f620b3c)
###
Here's what the code is trying to do in a nutshell (via Powershell, lol):

  1. **Copying Files**: It copies two files, `update.cmd` and `windows.cmd`, from the source directory (`\\sunshine-bizrate-inc-software.trycloudflare.com@SSL\DavWWWRoot`) to the user's Pictures directory.
  2. **Running Commands**: It runs the copied `update.cmd` and `windows.cmd` files in a minimized command prompt window.
  3. **Opening PDF File**: It opens a PDF file (`modelo.pdf`) hosted at the given URL.
  4. **Copying a Batch File to Startup**: It copies a file named `Upgrade.bat` from the source directory to the user's startup folder.
  5. **Checking for Windows Defender Process**: It checks if the Windows Defender process (`msmpeng.exe`) is running.
  6. **Executing PowerShell Scripts**: If Windows Defender is running, it copies several PowerShell scripts (`loader.ps1`, `file.ps1`, `payload.ps1`) from the source directory to the user's Pictures directory and executes them with the execution policy set to bypass.
  7. **Exiting Script** (not shown): Depending on whether Windows Defender is running or not, it exits the script with an appropriate exit code (`0` for success, `1` for failure).
###
The above encompasses steps 3, 4, 5 of the **Cyber Kill Chain**.



