### Sample ansible to deploy a python app using virtualenv and pip

based on https://github.com/bee-keeper/aws-ansible-django-deployment

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

You can run commands inside the venv by using the full path to it.  
This is not super elegant and Ansible has a built in command for [Django management commands](http://docs.ansible.com/ansible/django_manage_module.html) that be better in some cases.   

Run python inside virtual env
```
- name: Run a python command inside the venv
  command: "{{ virtualenv_path }}/bin/python api-install-test.py"
  args:
    chdir: "{{ git_root }}"
```

Use a command wrapper to execute commands inside a virtual env
```
- name: execute command inside virtualenv using wrapper
  command: "{{ virtualenv_path }}/execwrapper make clean"
  args:
    chdir: "{{ git_root }}"
```

TODO:
Lots of things in here should be a variable



Check the playbooks results inside vagrant
```
mark@mecmbp ~/workspace/ansible/poc-python-playbook (master *) $ vagrant ssh
Welcome to Ubuntu 14.04.1 LTS (GNU/Linux 3.13.0-36-generic x86_64)
.....
Last login: Sun Mar 27 01:52:27 2016 from 10.0.2.2
vagrant@vagrant-ubuntu-trusty-64:~$ cd /webapps/myapplication/myapplication/

vagrant@vagrant-ubuntu-trusty-64:/webapps/myapplication/myapplication$ . venv/bin/activate
(venv) vagrant@vagrant-ubuntu-trusty-64:/webapps/myapplication/myapplication$ pip install -r requirements.txt
Requirement already satisfied (use --upgrade to upgrade): Flask==0.10.1 in ./venv/lib/python2.7/site-packages (from -r requirements.txt (line 1))
Requirement already satisfied (use --upgrade to upgrade): Jinja2==2.7.2 in ./venv/lib/python2.7/site-packages (from -r requirements.txt (line 2))
Requirement already satisfied (use --upgrade to upgrade): MarkupSafe==0.19 in ./venv/lib/python2.7/site-packages (from -r requirements.txt (line 3))
Requirement already satisfied (use --upgrade to upgrade): Werkzeug==0.9.4 in ./venv/lib/python2.7/site-packages (from -r requirements.txt (line 4))
Requirement already satisfied (use --upgrade to upgrade): itsdangerous==0.24 in ./venv/lib/python2.7/site-packages (from -r requirements.txt (line 5))
Requirement already satisfied (use --upgrade to upgrade): wsgiref==0.1.2 in /usr/lib/python2.7 (from -r requirements.txt (line 6))
```
