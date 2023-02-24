# Ansible
Notes and scripts

# Ansible Install

### Operating System & Software
- Proxmox CT
- Ubuntu server 22.04
- Ansible

---

### Install Ansible on Ubuntu container
Update New Ubuntu Container Install
```
apt update && apt dist-upgrade -y
```

Install required software
```
apt install openssh-server sshpass python3 software-properties-common
```

Generate ssh keys for host and remote servers
```
ssh-keygen
```

Install and/or upgrade latest version of Ansible
```
python3 -m pip install ansible

python3 -m pip install --upgrade ansible
```


Install Ansible on Ubuntu Container from repository
```
add-apt-repository --yes --update ppa:ansible/ansible
apt install ansible
ansible --version
```

### Configure host and remote servers
Copy ssh keys to remote servers
```
ssh-copy-id USER@192.168.1.100
```

To run sudo command on remote server run the following command on remote servers
```
echo "$(whoami) ALL=(ALL) NOPASSWD:ALL" | sudo tee /etc/sudoers.d/$(whoami)
```

### Iventory file for remote servers
Edit Ansible host file
```
nano /etc/ansible/hosts
```

Add remote servers ip-address or domain name. Some examples:
```
[server01]
192.168.1.100
192.168.1.101

[server01:vars]
ansible_user=root
ansible_password=Pass@123
```
```
[servers02]
docker ansible_host=192.168.1.101
testbox ansible_host=192.168.1.102 ansible_user=box ansible_become=yes ansible_become_method=sudo
debian ansible_host=192.168.1.103 ansible_user=root ansible_password=Pass@123
```

### Ansible quick commands
Ping remote hosts
```
ansible -m ping all
```
Ping singe remote host
```
ansible -m ping 192.168.1.100
```
Ping single remote host as a specific user
```
ansible -m ping -u USERNAME 192.168.1.100
```
Ping group in inventory file
```
ansible -m ping GROUPNAME
```
Upgrade for root user
```
ansible -m shell -a 'apt update && apt dist-upgrade -y' docker
```
Upgrade for sudo users
```
ansible -b --become-method=sudo -m shell -a 'apt update' docker
```
Install a package
```
ansible -b --become-method=sudo -m shell -a 'apt install -y vim' docker
```

### Run playbook with command
```bash
ansible-playbook -i 192.168.1.100, -u root -k first_playbook.yml
```