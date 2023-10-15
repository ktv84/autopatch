# autopatch
Ansible is used for patching
Used for patching proxmox environment VMs and applications

Before using this repository you will need to create an ssh keypair and distribute the public key to the servers in the inventory list:
1. Create keypair
ssh-keygen -t ed25519

2. Distribute key to server
   ssh-copy-id ansible@10.0.1.2

3. Repeat step 2 for all your servers

4. Playbook will ask for sudo password on all servers. If you want to disable this do the following:
   sudo visudo
   $USER ALL=(ALL) NOPASSWD: ALL

HOW to patch:
Patch servers only: ansible-playbook patch.yml
Patch servers and force a docker container upgrade: ansible-playbook patch.yml -e docker=true
