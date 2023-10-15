# autopatch
##INFO
Ansible is used for patching
Used for patching proxmox environment VMs and applications

##PATCH SERVER AND HOSTS CONFIGURATION
Before using this repository you will need to create an ssh keypair and distribute the public key to the servers in the inventory list:
1. Create keypair
ssh-keygen -t ed25519

2. Distribute key to server
   ssh-copy-id ansible@192.168.0.2

3. Repeat step 2 for all your servers


##FILES THAT NEEDS TO BE CREATED MANUALLY
1. Create directory in this repository
> inventory
2. Create a file called hosts under this directory containing your hosts with with the groups proxmox, vm and docker. Example:
```
[proxmox]
192.168.0.2 ansible_user=ansible

[vm]
192.168.0.3 ansible_user=ansible

[docker]
192.168.0.3 ansible_user=ansible
```

##HOW TO PATCH USING ANSIBLE: 
  Patch servers only:
  > ansible-playbook patch.yml
  
  Patch servers and force a docker container upgrade (when docker host is not rebooted):
  > ansible-playbook patch.yml -e docker=true
