Adversaries frequently exploit public and temporary directories, such as `C:\Users\Public` and `C:\Users\UserName\AppData\Local\Temp`, as common drop zones to upload malicious tools and payloads. These directories are often targeted due to their accessibility and low visibility in standard security monitoring.

_**This project aims to monitor public and temporary directories for unauthorized file uploads and changes, detecting early signs of malware, privilege escalation, and insider threats.**_

### **Creating custom FIM rules**
https://documentation.wazuh.com/current/user-manual/capabilities/file-integrity/creating-custom-fim-rules.html

Firstly, we will need to configure `ossec.conf` file which is located under `C:\Program Files(x86)\ossec-agent` directory. </br> ( Copy the `ossec.conf` file as a backup before we changes the configuration file for best practice.)

![image01](https://github.com/user-attachments/assets/c622124a-1d05-4a2d-82df-db8bde1d2568)

Open the `ossec-conf`file with `Notepad` and go to `File Integrity Monitoring` part

![image02](https://github.com/user-attachments/assets/251abb4a-0a61-481b-b5a4-560fc1017120)

In this file, I added configuration for FIM to monitor these directories  `C:\Users\Public` , `C:\Users\*\AppData\Local\Temp` and `C:\Users\*\Documents` for every 1min. 

For more detailed configuration manual, please refer to

https://documentation.wazuh.com/current/user-manual/capabilities/file-integrity/index.html </br>
https://documentation.wazuh.com/current/user-manual/capabilities/file-integrity/creating-custom-fim-rules.html#custom-fim-rules-examples

![image03](https://github.com/user-attachments/assets/e7282042-90f7-44a6-bd13-62ea1e9da46d)

Restart the Wazuh service, after modifying the `ossec-conf`file

![image04](https://github.com/user-attachments/assets/215d5aa1-a008-4d74-a978-b118379765e6)

Verify if our directories are being monitored or not by creating/modifying/deleting some files under these directories. After creating/modifying your test files, go to Wazuh Dashboard and you will see events made by our tests.

![image05](https://github.com/user-attachments/assets/5db4fe4d-5a6e-4b32-b0f7-2ca98c2846d6)
![image06](https://github.com/user-attachments/assets/80b73503-8f43-4108-99c5-e40c5f39cca7)
![image07](https://github.com/user-attachments/assets/18566254-86e4-43d1-a673-cb7d19017743)

## Advanced FIM settings

### **Who-data monitoring**

The who-data functionality allows the FIM module to obtain information about who made modifications to a monitored file. This information contains the user who made the changes to the monitored files and the program name or process used.

https://documentation.wazuh.com/current/user-manual/capabilities/file-integrity/advanced-settings.html#who-data-monitoring-on-windows

### **Monitor changes in a text file on Windows**

Perform the following steps to configure the FIM module. This configuration gets the information about the user and the process that modified the monitored files.

1. Edit the Wazuh agent `C:\Program Files (x86)\ossec-agent\ossec.conf` configuration file and add the `Documents` directory for FIM monitoring. The configuration ensures that the FIM module records who-data information and also reports the exact changes made to text files:

![image08](https://github.com/user-attachments/assets/b40e3a4d-564e-42f1-ab4d-de0b52ef266f)

2. Restart the Wazuh agent using PowerShell with administrator privileges to apply the changes:

```markdown
Restart-Service -Name wazuh
```

After enabling whodata, we can view more detailed information about the system such as processid, username, differences made in the file, etc..

![image09](https://github.com/user-attachments/assets/73eace0f-3ce6-4c52-99bb-6ae97563e2b9)
![image10](https://github.com/user-attachments/assets/e60b4d72-2a01-4842-8195-8c04168be655)

### **Monitor privilege escalation activity**

We can also detect persistence activities by monitoring registry run key that are used to establish persistence. 

For more information, please refer to MITRE “**Boot or Logon Autostart Execution: Registry Run Keys / Startup Folder”**

https://attack.mitre.org/techniques/T1547/001/

![image11](https://github.com/user-attachments/assets/7ffcfd80-6a29-4dec-af23-e33c01558f88)

Run following example Powershell script to test persistence

```markdown
reg add "HKLM\Software\Microsoft\Windows\CurrentVersion\Run" /v updates /t REG_SZ /d "C:\Path\To\Malware.exe" /f
```
![image12](https://github.com/user-attachments/assets/fee771d6-8ef2-4d50-a4cb-c29f96c52be5)

New Registry Run Key has created on the system

![image13](https://github.com/user-attachments/assets/37cd30e1-5a0e-48dd-b4a8-d1b29916f2ac)

We can see this event on Wazuh FIM dashboard

![image14](https://github.com/user-attachments/assets/d8766e67-17fe-490e-a780-729f98829211)
![image15](https://github.com/user-attachments/assets/2fb152fb-e0a6-4cab-9625-a99d8436e030)
