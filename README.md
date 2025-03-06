# Hydra SSH Brute-Force Lab (Kali/Windows)

## Objective

Simulated an ethical brute-force attack on SSH credentials using Hydra on a Windows 10 Pro VM (`192.168.20.10`) from Kali Linux (`192.168.20.11`) in an isolated internal network, demonstrating authentication vulnerabilities for SOC training.

### Skills Learned
- Gained proficiency in network configuration and isolation for secure lab environments.
- Developed skills in vulnerability assessment and Red Team strategies using Hydra and Nmap.
- Enhanced Linux terminal and Windows administration expertise for cybersecurity tasks.
- Improved critical thinking in identifying and mitigating authentication threats.
- Mastered documentation and reporting for security assessments.

### Tools Used
- Kali Linux for penetration testing and Linux terminal operations.
- Hydra for brute-force credential attacks on SSH services.
- Nmap for network enumeration and service discovery.
- VirtualBox for creating and managing isolated internal network VMs.

## Steps
*Ref 1: Environment Setup* 

![Home Lab Design 1](https://github.com/user-attachments/assets/4f1197c0-a332-45d8-8e30-6645ed90c415)

*Description*: Shows the isolated internal network with Kali Linux VM (`192.168.20.11`) and Windows 10 Pro VM (`192.168.20.10`) on `192.168.20.0/24`, connected via VirtualBox, no internet access.

*Ref 2: SSH Enumeration*  

![SSH enumeration](https://github.com/user-attachments/assets/2b08be30-5296-436d-9b9e-5b0410679552)

*Description*: Displays Nmap output (`nmap -p 22 192.168.20.10`) confirming SSH (`22/tcp open ssh`) on the Windows VM, ready for attack.

*Ref 3: Wordlist Creation*  

![Wordlist Creation](https://github.com/user-attachments/assets/12ecc55e-cb7a-445e-abba-47b5c794964e)

*Description*: Shows the terminal command `echo -e "admin\npassword\nroot\ntest123" > wordlist.txt` creating the password list for Hydra.

*Ref 4: User Setup*  

![User Setup](https://github.com/user-attachments/assets/954c2367-a9f8-4de3-8bc1-583f2c221b1e)

*Description*: Illustrates the Windows Control Panel adding `portfolioproject:test123`, the weak target for the Hydra attack.

*Ref 5: Hydra Attack*  

![Hydra attack](https://github.com/user-attachments/assets/f3beb6cd-7790-4073-ae9f-780a4d420e98)

*Description*: Captures Hydra output (`hydra -l portfolioproject -P wordlist.txt 192.168.20.10 ssh`) cracking `portfolioproject:test123`.

*Ref 6: SSH Login Confirmation*  

![whoami](https://github.com/user-attachments/assets/f62af18b-5f02-48ff-b033-46888fa4bccd)

*Description*: Shows the SSH login `ssh portfolioproject@192.168.20.10` with `whoami` output (`portfolioproject`), verifying the breach.
