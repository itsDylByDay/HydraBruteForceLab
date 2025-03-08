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


## Lab Setup Details
- **Network Configuration**: Used VirtualBox’s “Internal Network” to isolate Kali (`192.168.20.11`) and Windows (`192.168.20.10`). Resolved initial IP conflicts by editing `/etc/network/interfaces` on Kali and IPv4 settings on Windows, ensuring `192.168.20.0/24` uniqueness.
- **SSH Installation**: Installed OpenSSH Server on Windows via `Settings > Apps > Optional Features` (online method). Started via `services.msc`,  no firewall adjustments were needed for pings after enabling ICMP, but SSH traffic worked by default on port 22.
- **Troubleshooting**: Faced “no route to host” for SSH—fixed by verifying Internal Network settings and rebooting VMs.

## SSH Enumeration Insights
- **Nmap Commands**: `nmap -p 22 192.168.20.10` confirmed `22/tcp open ssh`. Explored `nmap -p 22 192.168.20.0/24` to scan the full network, discovering all SSH-enabled devices—useful for SOC reconnaissance without a known IP.
- **Technical Note**: `-p 22` isolates SSH scanning. 'p' represetning the port in which SSH are hosted.

## Wordlist Creation Exploration
- **Methodology**: `echo -e "admin\npassword\nroot\ntest123" > wordlist.txt` created a simple list. Short for demo, but I plan a Python script that coould automate more complex password combinations.
- **Future Idea**: Automate with python to generate thousands of permutations, enhancing Hydra’s scope for SOC simulations.

## User Setup Details
- **Windows User**: Added `portfolioproject:test123` via Control Panel, ensuring SSH compatibility. Weak password mimics real-world misconfigurations SOC analysts target.
- **Verification**: Tested `ssh portfolioproject@192.168.20.10`—logged in successfully, confirming setup.

## Hydra Attack Analysis
- **Command**: `hydra -l portfolioproject -P wordlist.txt 192.168.20.10 ssh` cracked `portfolioproject:test123` instantly due to the small wordlist.
- **Performance**: Added `-t 4` to limit threads if slow; no issues here, but useful for SOC labs on larger networks.
- **Reflection**: Demonstrates brute-force risk—critical for SOC detection/mitigation training.

## Verification & Documentation Notes
- **SSH Confirmation**: `ssh portfolioproject@192.168.20.10` with `test123` and `whoami` verified access.
- **Mitigation**: Recommended strong passwords (e.g., 12+ chars, mixed types) and login limits (e.g., `fail2ban`) for SOC hardening.

## Outcome & Reflection
- **Success**: Proved weak credentials are exploitable, showcasing SOC threat assessment skills.
- **Learning**: Gained Linux terminal proficiency, virtual environment setup, and Red Team strategy insights. I’d automate wordlists and test larger networks for practical SOC scenarios.

## Troubleshooting Log
- **IP Conflict**: Both VMs initially shared `192.168.20.10`—fixed by static IP assignment.
- **SSH Issue**: “No route to host” resolved by verifying network, firewall, and SSH service status.
