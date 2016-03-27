###
Sample ansible to deploy a python app using virtualenv and pip

Vagrant playbook available.

### Required
You will need to install [Ansible](http://docs.ansible.com/ansible/intro_installation.html)  
If you want to test in Vagrant, you will need to install [Vagrant](https://www.vagrantup.com/docs/installation/)  

You can test the playbook using Vagrant  
```
$vagrant up
```

Once vagrant vm is built you can re-run playbook using  
```
$vargrant provision
```

Run the play book
```
$ ansible-playbook -i your-inventory.ini --private-key=/Users/mark/.ssh/gg_rsa --user=mconlin vagrant-main.yml
```
