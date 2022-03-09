# ansible-demo

pre-req: Vagrant, 

## Build 3 vagrant machines

### We are building 3 ubuntu servers,1 build server and 2web servers  
`vagrant up`

### Access build server using mobaxterm and make sure to include private key

### login to buildserver using user vagrant

### Update root password
`sudo passwd root`

### Switch user to root
`su root`

### Update system
`sudo apt update`

### Install ansible
`sudo apt install ansible`

### Update host file in buildserver
edit host file and add other server details ( this has to be in all servers)
`vi /etc/hosts`

    192.168.56.100 buildserver
    192.168.56.102 web01
    192.168.56.103 web02


### switch to vagrant user
`su vagrant`

## Create keys 
`ssh-keygen`
After running this command press enter with out proving any inputs.
Note: Files can be edited when we are using root user only.

### ssh copy id (switch to vagrant user and run)
this command will helps ansible to talk to other servers ( web01/web02) with out asking for passwords
`ssh-copy-id buildserver`
`ssh-copy-id web01`
`ssh-copy-id web02`
enter "yes" and password for vagrant user ( password is vagrant)

### Make new directoy playbooks and create a file called as "hosts"
[all]
buildserver
web01
web02

[webservers]
web01
web02

### Verify connetion whether we have access to webservers or not
`ansible webservers -i hosts -m command -a hostname -v`
`ansible webservers -i hosts -m command -a "df -h" -v`


## Clone my repo to local for testing 


### To run a playbooks with host file
ansible-playbook installhttpd.yaml -i ./hosts 

### This is a test change