

#  Setup Test Bed

## Install Requirements a boot environment
   - on Windows you will need hyperv enabled: see [Hyperv Setup guide](https://support.auvik.com/hc/en-us/articles/212801986-How-to-enable-Microsoft-Hyper-V-on-Windows-Servers-and-Workstations)
   - Windows users will also need wsl enabled. see this [guide](https://docs.microsoft.com/en-us/windows/wsl/install)
   - on wsl, install a ubuntu 20.04 service [from here](https://www.microsoft.com/en-gb/p/ubuntu-2004-lts/9n6svws3rx71?rtc=1&activetab=pivot:overviewtab)
   - You will need to install Vagrant on Windows, downloads found  [here](https://www.vagrantup.com/downloads)
   - next, navigate to the wsl console with command wsl on the console or the ubuntu shell.
   - install ansible in wsl Ubuntu with: 
   ```
   sudo apt-add-repository ppa:ansible/ansible
   sudo apt update
   sudo apt install ansible
   ```
   - Once ansible is ready go open a new administator Powershell console.
   - in Powershell (admin) navigate to the location of this repository.
   - on the same directory as the project, run:
     ```
      vagrant up 
     ```

## checking Hyperv

   - Once HyperV is running the environment, we need to capture the IP Address. From the HyperV applcation (can be found in search with HyperV), at the bottom of the page.
   Or from powershell enter the VM with
```
  vagrant ssh
  ifconfig 
```
  - Transfer your local ssh key to vagrant.
  - you will need to copy your local ssh key onto vagant box. First ensure you've got a ssh key generate. First, go to the Ubuntu WSL 2 console. with command wsl from a Windows terminal. Then run the below command
  ```
   ssh-keygen -t rsa
  ```
  Once you've generated a key, then we need to copy it to the vagrant box with: 
  ```
  ssh-copy-id -i ~/.ssh/id_rsa vagrant@<IP of Hyperv Box>
  ```
  - Now we're ready to run ansible playbook.

## Ansible Playbook
  
  - first update the ./inventory.ini file with the HyperV IP address.
  - From the Ubuntu console
  - navigate to ./ansible in the folder.
  - from ansible directory, run the following command:
  ```
  ansible-playbook --ask-become-pass -i ../inventory.yml nginxPlaybook.yml
  ```