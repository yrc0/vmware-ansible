
# VMWare-Ansible — Session 1 Lab Guide

## 0. Lab Goal
You will:
- Install & configure Ansible  
- Clone a Git repo  
- Understand repo structure  
- Install dependencies  
- Configure vCenter  
- Test connectivity  
- Run a VMware information playbook  

## 1. Prerequisites
- GitHub account  
- VS Code  
- VPN  
- vCenter hostname, username, password  
- Sample repo: https://github.com/sample/vmware-ansible  

## 2. Windows Setup (WSL)
### Install WSL:
```
wsl --install -d Ubuntu
```

### Install tools:
```
sudo apt update
sudo apt install -y ansible git python3-pip
```

### Clone repo:
```
git clone https://github.com/rsr0001/vmware-ansible.git
```

### Install pyvmomi:
```
python3 -m pip install --user "pyvmomi>=8.0.0" --break-system-packages
```

### Install VMware collection:
```
ansible-galaxy collection install community.vmware
```

## 3. macOS Setup
### Install Homebrew:
```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

### Install:
```
brew install git ansible python
```

### Clone repo:
```
git clone https://github.com/sample/vmware-ansible.git
```

### Install pyvmomi:
```
python3 -m pip install --user pyvmomi
```

## 4. Configure vCenter
```
cp group_vars/vcenter.yml.example group_vars/vcenter.yml
```

Edit values accordingly.

## 5. Inventory File
```
all:
  children:
    vcenter:
      hosts:
        vcenter1:
          ansible_host: "vc01.example.local"
          ansible_connection: local
```

## 6. Connectivity Test
```
ping -c 4 vc01.example.local
```

## 7. Test Playbook
```
ansible-playbook -i inventory.yml playbooks/vcenter_about.yml
```

## 8. Completion Checklist
- Repo cloned  
- vcenter.yml configured  
- pyvmomi installed  
- VMware collection installed  
- VPN connectivity OK  
- Playbook executed  
