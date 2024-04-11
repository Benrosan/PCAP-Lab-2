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
The host then starts looking for a specific batch file: **file.bat** via PROPFIND method. 
###
Once the file is found, the host downloads the file. Following the TCP Stream on the GET method shows the Python code that's contained on the batch file and executed on the host:
###
![2024-04-11 12_29_55-Kali Linux on GENIE - Virtual Machine Connection](https://github.com/Benrosan/PCAP-Lab-2/assets/160042310/3576d8da-7cd5-4743-9fc3-dbd44f620b3c)
###
Here's what the code is trying to do:




