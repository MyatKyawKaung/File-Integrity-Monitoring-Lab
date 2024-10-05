<h1 align="center">File Integrity Monitoring System</h1>

## Description
This project aims to monitor critical files from unauthorized modifications, ensuring data integrity and preventing security breaches. The primary goals are to: <br>

* Detect and alert users to any changes made to monitored files.
* Record historical changes for auditing and analysis.
* Provide a customizable and efficient monitoring solution.

## Key Features
* Real-time file monitoring: Continuously tracks changes to specified files or directories.
* Customizable alerts: Allows users to configure email, SMS, or other notification methods.
* Detailed change logs: Records information about modifications, including timestamp, user, and changes made.

## Prerequisites
* **Ubuntu Server**: This will host Wazuh server and utilize Wazuh FIM module. </br>
* **Windows Server** : This will use as a target machine to detect files modifications.
