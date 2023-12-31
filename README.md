# autopatch
## INFO
- Used for patching proxmox environment VMs and applications
- Ansible is required
- Optional docker container patching implemented


## PATCH SERVER AND HOSTS CONFIGURATION
Before using this repository you will need to create an ssh keypair and distribute the public key to the servers in the inventory list:
1. Create keypair
```sh
ssh-keygen -t ed25519
```

3. Distribute key to server
```sh
ssh-copy-id ansible@192.168.0.2
```

5. Repeat step 2 for all your servers


## FILES THAT NEEDS TO BE CREATED MANUALLY
1. Create directory in this repository
```sh
inventory
```
And create a file called hosts under this directory containing your hosts with with the groups proxmox, vm and docker. Example:
```ini
[proxmox]
192.168.0.2 ansible_user=ansible

[vm]
192.168.0.3 ansible_user=ansible

[docker]
192.168.0.3 ansible_user=ansible

[dockerint]
192.168.0.4
```
2. Create directory in this repository
```sh
group_vars
```
And create a file called docker and dockerint under this directory containing the username used by the docker service. Example:
```ini
docker_user: docker
```

## HOW TO PATCH USING ANSIBLE: 
Patch servers only:
```sh
ansible-playbook patch.yml
```
  
Patch servers and force a docker container upgrade:
This needs to be run in the following scenarios:
- When host OS is not rebootet and containers need an upgrade (pull from remote)
- When you have a new container or compose configuration you need to apply
```sh
ansible-playbook patch.yml -e docker=true
```
