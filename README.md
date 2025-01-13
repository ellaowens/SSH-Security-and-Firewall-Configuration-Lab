<h1 align="center">SSH Security and Firewall Configuration Lab:</h1>

In this lab, I established an SSH connection from macOS to an Ubuntu server and demonstrated key techniques for securing a Linux system. The lab focused on hardening SSH access by disabling root login, configuring key-based authentication, and restricting access to the server. I also implemented firewall rules using UFW, allowing only necessary services while blocking all other traffic. Additionally, I tested network configurations with tools like Nmap and Netcat to verify security measures. This project highlights my ability to manage secure remote access and configure network security in a Linux environment.

##

Steps:

- **Enabled SSH services on the terminal**
  - _Sudo apt update && sudo apt upgrade -y_ (Check for updates & upgrades, if needed)
        
- **Installed open SSH server**
  - _Sudo apt install openssh-server_
        
- **Checked to make sure ssh is actually running**
  - _Sudo systemctl status ssh_
  - _ip a_ (to find server's ip address)
    <img width="798" alt="Screenshot 2025-01-12 at 10 34 54 PM" src="https://github.com/user-attachments/assets/df2ea0a4-57c6-4ef4-9bdc-4514cc15c8f3" />
        <img width="561" alt="Screenshot 2025-01-12 at 10 48 56 PM" src="https://github.com/user-attachments/assets/5bb09042-7e9d-4049-a22b-44cc2eef17d8" />

- **Opened my Mac’s terminal** (I have used PuTTy for a pervious project)
  - _Ping 192.168.64.11_ (my Ubuntu server’s ip) to see if it is working properly
  - _ssh -v ella@ubuntuu_ or _ssh ella@192.168.64.11_ to successfully SSH into my Ubuntu server
    <img width="1428" alt="Screenshot 2025-01-13 at 11 47 31 AM" src="https://github.com/user-attachments/assets/a4cbae56-5968-4e0a-8807-bdd66323fb7d" />
    <img width="482" alt="Screenshot 2025-01-13 at 11 50 57 AM" src="https://github.com/user-attachments/assets/a21c2dbe-3cf0-4c6d-97f2-32ec7a046fc1" />
    <img width="485" alt="Screenshot 2025-01-13 at 11 53 22 AM" src="https://github.com/user-attachments/assets/3bf35ad8-8d17-4bd0-a582-647eb98fecb2" />


        
**- Ran a few commands in the Ubuntu server**
  - _Whoami_
  - _Uname -a_
  - _Ls_(to view the files in my current directory)
  - _Exit_ (to exit the SSH session)

    <img width="554" alt="Screenshot 2025-01-12 at 11 31 21 PM" src="https://github.com/user-attachments/assets/2b909c12-206e-4113-a7fa-d1229fdc3bbf" />
    <img width="484" alt="Screenshot 2025-01-12 at 11 32 17 PM" src="https://github.com/user-attachments/assets/4857711a-41e0-4a6c-9d3a-c66e559a5296" />
 ##

<h3 align="center">Setting Up Firewall (UFW) on Ubuntu Server:</h3>

Steps: 

- **Ensured UFW is installed and active on my Ubuntu server**
  - _sudo apt update && sudo aot install ufw_
    
   <img width="576" alt="Screenshot 2025-01-13 at 12 04 46 PM" src="https://github.com/user-attachments/assets/b542b35f-f430-4a16-ab3d-662a74cc22c9" />

**- Allowed SSH access**  
- _sudo ufw allow ssh_
 
**- Denied all other incoming traffic**
  - _sudo ufw default deny incoming && sudo ufw default allow outgoing_
    
   <img width="821" alt="Screenshot 2025-01-13 at 12 05 50 PM" src="https://github.com/user-attachments/assets/5ed7c1ee-478e-426b-81df-ce94356c0071" />

**- Enabled UFW and checked status**
  - _sudo ufw enable_
  - _sudo ufw status verbose_
    
     <img width="498" alt="Screenshot 2025-01-13 at 12 06 26 PM" src="https://github.com/user-attachments/assets/692b6688-afcd-4c31-b61c-d9c8c058623e" />

    <img width="587" alt="Screenshot 2025-01-13 at 12 06 57 PM" src="https://github.com/user-attachments/assets/1c9666a9-4cfb-4729-8f33-5652fc47983a" />

##
**SSH Hardening**

**- Opened the SSH configuration file**
  - _sudo nano /etc/ssh/sshd_config_
  - change PermitRootLogin to no
    
    <img width="838" alt="Screenshot 2025-01-13 at 12 08 28 PM" src="https://github.com/user-attachments/assets/41bbeda4-25b7-402d-b4af-7deedbd41546" />
    <img width="240" alt="Screenshot 2025-01-13 at 12 09 02 PM" src="https://github.com/user-attachments/assets/a125783f-01c3-4cce-b279-c9ed5e2b596c" />


**- Restart the SSH service to apply changes**
  - _sudo systemctl restart ssh_

## 
**Test the Connectivity**

- **Tested the SSH connection on my macOS terminal**
  - _ssh ella@192.168.64.11_
 <img width="476" alt="Screenshot 2025-01-13 at 12 26 20 PM" src="https://github.com/user-attachments/assets/6faa2982-f17a-4411-a1d4-498f0419855f" />

**- Used nmap on my macOS terminal to check for open ports (only port 22 should be open)**
  - _nmap -sS 192.168.64.11_ 

**- Used netcat to test if the server can communicate over specific ports**
   - _nc lvp 1234_
  <img width="195" alt="Screenshot 2025-01-13 at 12 30 06 PM" src="https://github.com/user-attachments/assets/6f8fc11d-caaa-4656-bdb1-6a329de9630c" />

**- Send data from my macOS terminal**
  - _nc 192.168.64.11 1234_
 <img width="248" alt="Screenshot 2025-01-13 at 12 43 45 PM" src="https://github.com/user-attachments/assets/c9a1779f-c3e0-4da2-8614-9793ae407de3" />

##
**Monitoring Logs**

**- I reviewed login attempts:**
  - _sudo tail -f journalctl_ (or _/var/log/auth.log_)
  <img width="837" alt="Screenshot 2025-01-13 at 12 45 15 PM" src="https://github.com/user-attachments/assets/6a8210c4-0a92-48fc-82b7-e6f9a791cbf9" />

