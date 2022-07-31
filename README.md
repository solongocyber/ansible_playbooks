
# Ansible2022
### What is Ansible?

Ansible is an open source IT configuration management (CM) and automation platform or tool, provided by Red Hat. It uses human-readable YAML templeates so that users can program repetitive tasks to pure automatically, without learning an advanced language. 

 ### What is YAML ?

* YAML stands for Yet Another MArkup Language. 
* It's a data serialization language that is often usesd for writing configuration files.
 * YAML is exceptionally human-readable syntax. 
 * All YAML files begin with --- and end with ... these are indicates the start and end of a document.
 * Each key-value pairs separated by ':'

 ## Introduction to ad hoc commands

 An Ansible ad hoc command uses the /usr/bin/ansible command line tool to automate a single task on one or more managed nodes.Ad hoc commands are quick and easy but they are not reusable. 
 #### Why use ad hoc commands?
 Ad hoc commands are great gor tasks you repeat rarely, you could execute a quick one- liner in Ansible without writing a playbook. An ad hoc command looks like this:
 ```
 ansible localhost -m "module" -a "module options"
 ```
### Use cases for ad hoc tasks
 Ad hoc tasks can be used to reboot servers, copy files, manage packages and users, and much more. You can use any Ansible module in an ad hoc task. ad hoc tasks, like playbooks, use a declarative model, calculating and executing the actions required to reach a specified final state. They achieve a form of idempotence by checking the current state before they begin and doing nothing unless the current state is different from the specified final state.

For example using ad hoc command and installing apache:
```
ansible localhost -m yum -a "name=httpd state=latest"
```
ansible [pattern] -m [module] -a [module options]

**`ansible`** - 
**` localhost`** - [pattern]. It's name of the host 

**`-m`** [module_name]- `yum` is a  module

**`-a`** [module_options] "name=httpd state=latest"


## Managing files
### Using `copy` module to transfer a file directory to localhost server 
```
ansible localhost -m copy -a "src=/etc/hosts dest=/tmp/hosts"
```
### Using `file` module allows changing ownership and permissions on files

```
ansible localhost -m file -a "dest=/var/www/html mode=600 owner=apache group=apache"
```
Delete directories (recursively) and delete files

```
ansible localhost -m file -a "dest=/path/to/file or dir  state=absent"
```

## Managing package

Using ad-hoc to install , update, or remove packages on host server using a package manager module like `yum`:
```
ansible localhost -m yum -a name=httpd state=installed
```

## Managing user and groups

Create, manage and remove user accounts on your managed hosts with ad-hoc task using `user` module:

```
ansible all -m user -a "name=foo pasword=here"
```
## Managing services

Ensure a service is started on host using service module:

```
ansible all -m service -a "name=httpd state= started"
```


### Ansible_facts

Gathering Facts means ansbile get some metadata about server from Gathering Facts ansible fact has default variables:

``` 
ansible localhost -m setup

```

```
ansible localhost -m setup -a " filter=*family*"
```
how to create ansible facts in playbook see variables.yaml

Debug module prints statements during execution and it will show on screen.
It is very useful with WHEN statment.

Debug module can have parameter msg or var: see examples in variable.yaml file


Register is used to create variables from the output of an Ansible task. We can use registerd variable in later tasks in your play. But it is stored in memory so it cannot used future playbook, only in during execution.

[Click here : More about Ansible](https://www.redhat.com/en/technologies/management/ansible/what-is-ansible)

[Click here: Ansible Documentation](https://docs.ansible.com/)





![this is playbook](https://linuxbuz.com/wp-content/uploads/2020/07/ansible-playbook-feature.png)
playbook
Playbooks are the file where Ansible code is written. Playbooks are written in YAML format. Playbooks are customizable scripts that are used to execute a series of tasks and commands. They are like a to-do list for Ansible and tell what to do when it connects to each machine. 

Ansible runs tasks on hosts, with SSH connection established. It runs in ansible server, opens up SSH connection to your remote hosts and then runs commands directly on them.

### What is task?
A task can be anything from creating resources in AWS Cloud , to launching an instance, installing packages on a server, updating a config file or checking the time on a remote host.
By default , Ansible execute each task in order, one at a time, agains all machines matches by the host. 

### What is host?

The host is where the task get run. It can be any number if remote hosts that you have SSH access to, or localhost. YOur hosts respective IP address or hostnames need to be stored in an inventory file for Ansible to be aware of them. 

Desired state and       ***`Idempotency`***

Most Ansible modules check whether the desired final state has already been achived, and exit without performing any action  so that repeating the task does not change the final state. Wheter you run a playbook once, or multiple times, the outcome should be the same. 
Most Ansible modules check whether the desired final state has already been achived, if it has been achived exit without performing any action  so that repeating the task does not change the final state. Wheter you run a playbook once, or multiple times, the outcome should be the same. 
 
 
 YAML is a strict typed language; so extra care needs to be taken while writing the YAML files.
A YAML starts with --- (3 hypens)

Playbook example :

<img width="1005" alt="Screen Shot 2022-07-09 at 8 58 24 PM" src="https://user-images.githubusercontent.com/63433671/178128447-2717a031-c164-43c7-99ca-d57173ceeb81.png">


Checking syntax errors before run the playbook with below command:
```
ansible-playbook copy_passwd.yaml --syntax-check

``` 
To run your playbook, use the ansible-playbook command:

```
ansible-playbook copy_passwd.yaml 

```
If there is no error, result will be :
<img width="1029" alt="Screen Shot 2022-07-09 at 8 57 47 PM" src="https://user-images.githubusercontent.com/63433671/178128465-422cb0e3-5bd0-4a8c-a715-4bc76ffacfdd.png">


Make sure check the output

<img width="765" alt="Screen Shot 2022-07-09 at 8 47 21 PM" src="https://user-images.githubusercontent.com/63433671/178128412-e76828fd-27f1-4bd2-bd05-d05b5dfd6b37.png">

<img width="760" alt="Screen Shot 2022-07-09 at 9 03 25 PM" src="https://user-images.githubusercontent.com/63433671/178128430-ce03582d-07db-4ace-ac3a-4b3816779232.png">




[Get more about Ansible playbook, click here](https://docs.ansible.com/ansible/latest/user_guide/playbooks_intro.html)


