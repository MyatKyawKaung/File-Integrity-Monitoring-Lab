**In this demo, I will be using DigitalOcean cloud provider for my infrastructure and follow the official Wazuh documentation as a reference.**

https://documentation.wazuh.com/current/installation-guide/wazuh-server/installation-assistant.html

Create a droplet (VM) to install Wazuh Server

![image01](https://github.com/user-attachments/assets/8b0753a3-84b2-416c-a187-d47970a46860)

Select a Region where your VM will be created

![image02](https://github.com/user-attachments/assets/e14207f9-bc5a-4b92-bd45-338fcf338973)

Select a VPC for your VM. (You can leave it with a default VPC subnet but for me I created a New VPC subnet for this lab)

![image03](https://github.com/user-attachments/assets/b3f5c01a-c5be-48c3-be95-970ec828760b)

Choose your Image, version and resource type

![image05](https://github.com/user-attachments/assets/862cadab-4927-4b80-81ee-8a2fd229963b)

For CPU sizing, I chose regular disk type and 4GB/2CPUs which is enough for this lab

![image06](https://github.com/user-attachments/assets/01105506-63bf-46f1-9a91-de699586c0a4)

For Authentication Method, I chose `Password` for the sake of simplicity. You can generate and set up your SSH keypair using PuttyGen as well

![image07](https://github.com/user-attachments/assets/29c642d8-5783-47a4-903f-cea62103b7af)

Give a hostname for your Wazuh server and hit `Create Droplet`

![image08](https://github.com/user-attachments/assets/a92e4bff-e19b-4f1f-b29f-15969f59e8a6)

Once VM has created, we will need to add Firewall rules to only accept port 22 from our IP addresses to prevent malicious actors from brute forcing Wazuh Server

Under Manage Tab > `Networking` > `Firewalls` > `Create Firewall`

![image09](https://github.com/user-attachments/assets/ab7d02a8-7086-4589-a65b-2db0e0e4fa51)

Create an Inbound Rule and only allow your IP address for SSH

![image10](https://github.com/user-attachments/assets/8eb36b30-f799-4491-8bce-6f5ad05b134f)

Add your droplet to the firewall you have previously created

![image11](https://github.com/user-attachments/assets/5d67b789-726c-4d30-9f4b-0e97c9f74841)
![image12](https://github.com/user-attachments/assets/1660e4a5-55a0-4579-9a81-23a896d7c9fd)


SSH into your Wazuh Server from droplets

![image13](https://github.com/user-attachments/assets/5aa3de66-5840-4287-8203-299a52399e3e)

Once you have SSH into your VM, update and upgrade your Ubuntu instance

![image14](https://github.com/user-attachments/assets/54dd1d39-c901-4c45-84ac-577054aae525)

### Install Wazuh 4.9

```markdown
curl -sO https://packages.wazuh.com/4.9/wazuh-install.sh
```

```markdown
bash wazuh-install.sh http://wazuh-install.sh/ -a
```
![image15](https://github.com/user-attachments/assets/8a6684cb-f3cf-4296-8086-3bbe84dc8af5)

Make sure to save your username and password to login Wazuh-Dashboard from the web

![16](https://github.com/user-attachments/assets/19c5d653-6343-4ca3-90e9-3aaa5279b72f)

Login with the username and password from Wazuh installation. You will be directed to Wazuh Overview dashboard

![image17](https://github.com/user-attachments/assets/e7952522-5efa-4727-90f9-e97ddc0550f9)
![image18](https://github.com/user-attachments/assets/6af74e04-25fb-490d-bf02-7e99855c4765)
