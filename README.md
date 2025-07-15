# 🔍 Detecting Malicious PowerShell Activity with Sysmon

## 📌 Objective
Demonstrate how **Sysmon** can be used to detect the execution of **Base64-encoded PowerShell commands** run via **Command Prompt**, providing visibility into potentially obfuscated or malicious behavior on a Windows system.

---

## 🧠 Introduction
Attackers often encode PowerShell commands to bypass detection and obscure their activity. In this project, I simulate this tactic and show how **Sysmon** logs provide detailed forensic evidence — including command-line arguments, parent processes, and integrity levels — which can help detect such behavior.

---

## 🛠 Methodology

### 🔐 Step 1: Encode PowerShell Command
Used PowerShell to encode a simple command:

```powershell
[Convert]::ToBase64String([Text.Encoding]::Unicode.GetBytes('Write-Output "hello world"'))
```
<img width="1920" height="1014" alt="powershell_base64" src="https://github.com/user-attachments/assets/c4f4390a-8449-499a-8545-a364ffed3d41" />

Step 2: Execute Encoded Command via CMD

Executed the encoded command from Command Prompt using:
```powershell -EncodedCommand <Base64EncodedString>
```
<img width="1920" height="1014" alt="cmd_base64_helloworld" src="https://github.com/user-attachments/assets/bad2bac6-87ae-45aa-8842-4d6f3fe57ff1" />

Step 3: Monitor with Sysmon
Sysmon (System Monitor by Microsoft Sysinternals) was used to log process creation events.

Checked Event ID 1 under the Sysmon Operational Log in Event Viewer.

<img width="1920" height="1014" alt="sysmon-project3" src="https://github.com/user-attachments/assets/ee41ed02-829f-4942-96ad-30290284e142" />


Captured Details:

Execution of powershell.exe with the -EncodedCommand argument.

Parent process: cmd.exe

Integrity level: High

Full command line and hash values were logged.

Conclusion
This project confirms that Sysmon is highly effective for detecting suspicious PowerShell activity, particularly when commands are encoded to evade basic detection. Security analysts can use this approach to identify and investigate potential threats more effectively.

Tools Used
Windows 10

Sysmon

PowerShell

Windows Event Viewer
