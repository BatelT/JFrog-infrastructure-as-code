## Steps


### Prereqs

* Ansible and Terraform installed on your machine.
* A pair of SSH keys.

### Terraform

First off, hop over to the Terraform directory.
```
cd terraform/
```
Run the `init.sh` script to initialize the required values.
```
chmod +x init.sh
./init.sh
```

Begin Terraforming!
```
terraform init
```
```
terraform plan
```
```
terraform apply
```
Store the ip address of the newly created compute instance in a variable, we will be using it shortly.
```
export VM_IP=$(terraform output ip)
```

### Ansible

Add the following line to Ansible's inventory, either `/etc/ansible/hosts` or a custom file. Be sure to pass in the newly minted IP address and your SSH private key.
```
[artifactory]
<artifactory_IP> ansible_ssh_private_key_file=<Path_to_Private>
```

Switch over to the Ansible directory.
```
cd ansible/
```
Run the `init.sh` script to initialize the required values.
```
chmod +x init.sh
. ./init.sh
```
Check that Ansible can connect to your VM.
```
ansible atrifactory -m ping
```
Run the playbooks!
```
ansible-playbook playbooks/main.yaml
```




