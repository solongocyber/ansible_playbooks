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


