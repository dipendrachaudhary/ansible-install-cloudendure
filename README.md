# Ansible playbook to install and configure cloudendure in linux and windows machine


## Requirement for source machine
* The installation requirements for Source machines depend on the type of OS that the machine runs – either Linux or Windows.


## Installation Requirements for Linux Source Machine: Verify the following configuration
* Python is installed on the machine
* Verify that you have at least 2 GB of free disk on the root directory (/) of your Source machine for the installation. To check the available disk space on the root directory, run the following command: df -h /
Free disk space on the /tmp directory – for the duration of the installation process only, verify that you have at least 500 MB of free disk on the /tmp directory. To check the available disk space on the /tmp directory run the following command: df -h /tmp
* The active bootloader software is GRUB 1 or 2.
* Ensure /tmp is mounted as read+write.
* The CloudEndure user needs to be either a root user or a user in the sudoers list.
* Ensure that dhclient package is installed. If not, install the package. (run yum install dhclient in CMD)
* Verify that you have kernel-devel/linux-headers installed that are exactly of the same version as the kernel you are running.


## Installation Requirements for Windows Source Machine: Verify the following configuration
* (For replicating machines to AWS cloud only) - .NET Framework version 4.5 or above is installed on machines running Windows Server 2008 R2 or higher. .NET Framework version 3.5 or above on machines running Windows Server 2008 or lower.
* Windows Source machines need to have at least 2 GB of free space during Target machine launch in order to successfully launch a Target machine

* You can learn about the requirements here
```
https://docs.cloudendure.com/Content/Installing_the_CloudEndure_Agents/Agent_Installation_Requirements/Agent_Installation_Requirements.htm
```


## Note
* You need to have all the prerequisites installed in both ansible and nodes before running the command
* Update your Linux and Windows IP and credentials in inventory/hosts


## Linux task

* At first step the playbook downloads cloudendure installation file in the remote machin
* It runs the installation file to install cloudendure. To run installation, run the following command
```
ansible-playbook -i inventory/hosts master.yml --extra-vars "role_name=linux run_option=install";
```
* It also runs uninstallation. To run uninstallation run the following command
```
ansible-playbook -i inventory/hosts master.yml --extra-vars "role_name=linux run_option=uninstall";
```




## Windows task

* At first step, the playbook downloads the installation file in the remote machine
* It runs the installation file. Run the following command to install cloudamize in Windows.
```
ansible-playbook -i inventory/hosts master.yml --extra-vars "role_name=window run_option=install";
```
* It also runs uninstallation. Run the following command to uninstall cloudamize in Windows.
```
ansible-playbook -i inventory/hosts master.yml --extra-vars "role_name=windows run_option=uninstall";
```

## Vars

* become_user_linux denotes which the user of the remote machine
* cloudendure_agent_path is the path for the agent in linux that verifies if cloudendure is installed and runs the commands accordingly
* linux_cloudendure_download_url denotes the url to download the cloudendure installation file
* linux_cloudendure_download_destination denotes the destination where the file will be downloaded in the remote machine
* linux_cloudendure_install_file is the command to install cloudendure in linux
* linux_cloudendure_directory is the location for the installation file so the command will run in this directory
* linux_installation_file_path is the path for the installation file which is deleted after installation is is complete
* linux_cloudendure_run_uninstall_1 is the command to stop the cloudendure agent in linux
* linux_cloudendure_run_uninstall_2 is the command to remove cloudendure in linux

* windows_cloudendure_agent_path is the path to verify if the cloudendure is installed
* windows_cloudendure_download_url to download cloudendure in windows
* windows_cloudendure_download_destination denotes the destination for the downloaded file.
* install_cloudendure_in_windows denotes the command to run the downloaded file in windows to install cloudmize. You can replace the customerkey with yours
* windows_cloudendure_uninstallation_directory_source is the source of the directory where the file to uninstall cloudendure lies
* windows_cloudendure_uninstallation_directory_destination is the destination where the uninstallation file for cloudendure is copied to run
* uninstall_cloudendure_in_windows is the command to remove cloudendure in windows
* windows_cloudendure_uninstallation_file_destination is the directory where the uninstallation command for cloudendure runs


## Inventory

* You can edit the inventory file in inventory/hosts
