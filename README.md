[Set Up](doc/SetUp.md) | [Folder Structure](doc/lab-001.md) | [Mysql Role](doc/lab-002.md) | [Apache Role](doc/lab-003.md) | [Using Facts](doc/lab-004.md) | [Ansible Vault](doc/lab-005.md)

# SetUp ~ Installing and Setting up hosts

#### Pre-Requisites:
- __Vagrant__
- __Virtualbox__
- __git__
- __Putty (if you are on windows)__

### Clone the following repo:

`git clone https://gitlab.com/Pudd1ng/AnsibleMeetUp`

### Bringing up the environment:

Cd into the new repository and run the command `vagrant up`

### Installing Ansible:

Once the environment is up and running we should be able to ssh into our new,
machines run the command `vagrant ssh control` to enter our ansible control
machine

Vagrant should have already installed and copied all the files we require for
Ansible to run. However we still need to set up our nodes!

### Configuring Ansible:

Open another terminal session and cd into the new repository. From here ssh
into our desired nodes `vagrant ssh database`. A Enter the command ifconfig and
take note of the ip under eth1

Go back to our ssh session in our control machine and open the following hosts
file `sudo vim /ansible/hosts` 

Inside this file write the following:
```yaml
[control]
localhost ansible_ssh_user=vagrant ansible_ssh_pass=vagrant

[database]
'databaseip' ansible_ssh_user=vagrant ansible_ssh_pass=vagrant
```
__Note that databaseip will be the ip of your database machine__

We also need to set up an ssh key into our node from our control machine. From
the control machine type the following command `ssh vagrant@localhost`
the password should be vagrant.

As we want to communicate to our Database node do the same for that as well 
`ssh vagrant@database`
The password should also be vagrant.

### Testing our connections:

First lets see if our inventory has our hosts in. Inside /ansible run `ansible
--list-hosts all` you can also run this against hosts groups for Instance
running `ansible --list-hosts database` should show only our new node ip

Now we can see Ansible taking in our host information lets test the SSH
connections. Run the command `ansible -m ping all` to see if our control machine
gets a response from each box

### Short Instructions
1. `git clone https://gitlab.com/Pudd1ng/AnsibleMeetUp`
2. `cd AnsibleMeetUp`
3. `vagrant ssh control`
4. __Open a new session__
5. `cd AnsibleMeetUp`
6. `vagrant ssh database`
5. `ifconfig`  **Note the iP**
6. __In the control terminal__ `sudo vi /ansible/hosts`
7. **Add the above code**
8. `ssh vagrant@localhost`
9. `ssh vagrant@databaseip`
10. `ansible --list-hosts all`
11. `ansible -m ping all`
