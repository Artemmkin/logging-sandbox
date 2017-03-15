_These roles assume that you run ubuntu14.04. I used AWS for my tests_


### How to use these roles?

There is a separate role for each service you want to install and play around with.

Normally the order of the steps you should take would like this:  
1. Setup Storage and Log Indexer (Elastic Stack, Graylog):

    There is a role and a playbook for each ```storage+indexer``` host: ```elk```, ```graylog```.

2. (optional) Install a Message Broker on a separate host:

    There is a role for each Message Brokers to install: ```kafka```, ```redis```. Change ```broker.yml``` playbook to define which one you want to install.
3. Install some service (nginx, apache2, etc) on a separate host along with a shipper.

  There is a role for each ```log shipper``` and a role for ```services``` which installs services we specify in ```install_services``` variable inside ```log-generator.yml``` playbook. In the same playbook, we specify which _log shipper_ we want to install. Note, that some roles, like ```filebeat```, require a few variables to be set before running, so please see a role's readme file first before running anything.


### Things you have to chagne

You'll have to change ```ansible.cfg``` file and make sure you have a correct path to the ssh key:
```
private_key_file = ~/.ssh/express42
```

Also, change hosts ip addresses inside the ```hosts``` file.
```
elk ansible_host=<public_ip_address> ansible_user=ubuntu
```

Playbooks, that you want to run are listed inside ```site.yml``` file.

### How to run?

You can use a command like the one bellow to run all the playbooks you specified inside ```site.yml```:
```
ansible-playbook site.yml
```

to run just one specific playbook, you can use this command:

```
ansible-playbook playbook/<name_of_playbook>
```
