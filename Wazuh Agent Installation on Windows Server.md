## Installing Wazuh Agents on Target Windows Server
 
**_Note: For more detailed deployment variables for Windows Wazuh Agent Installer, you can reference from Wazuh official documentation websites_**

https://documentation.wazuh.com/current/installation-guide/wazuh-agent/wazuh-agent-package-windows.html
https://documentation.wazuh.com/current/user-manual/agent/agent-enrollment/deployment-variables/deployment-variables-windows.html 


On your Wazuh Manger dashboard, go to `Server Management` > `Endpoint Summary`> `Deploy new agent`

![image01](https://github.com/user-attachments/assets/ea1c905f-ae84-4722-a36f-3dffb4d28934)


Choose Windows package and add your Server IP address

![image02](https://github.com/user-attachments/assets/600dba87-61ff-4594-9291-e47773395a3b)


Add your Wazuh Agent name, copy the following command and run Powershell as Administrator on your `WindowsServer2019`

![image03](https://github.com/user-attachments/assets/24a6ca04-9d87-43b1-89f1-bb345e10d88b)

```markdown
Invoke-WebRequest -Uri https://packages.wazuh.com/4.x/windows/wazuh-agent-4.9.0-1.msi -OutFile ${env.tmp}\wazuh-agent; msiexec.exe /i ${env.tmp}\wazuh-agent /q WAZUH_MANAGER='152.42.236.56' WAZUH_AGENT_NAME='WindowsServer2019' 
```

![image04](https://github.com/user-attachments/assets/d181b9c7-9f52-4992-9d69-68a59730b1c2)

Once you finished downloading, install Wazuh agent and start Wazuh service

```markdown
NET START WazuhSvc
```

![image05](https://github.com/user-attachments/assets/1b1e953d-2a0c-43ac-874f-da63fa86abb5)

You can verify Wazuh service is running or not by running `services.msc` in run box

![image06](https://github.com/user-attachments/assets/d0928dbb-d157-48a6-b3f3-655e90c474c8)

You can view Wazuh Agent’s status on Wazuh Endpoints Security Dashboards

![image07](https://github.com/user-attachments/assets/ecb38d9b-ebfe-4f53-9425-a14c32713944)
![image08](https://github.com/user-attachments/assets/b5e27d96-e19d-4fbb-96e0-905f1af775d9)
![image09](https://github.com/user-attachments/assets/1a595a06-b6d0-4c0c-8cdb-6f3d10397e04)

