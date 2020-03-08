# What is it ?
Another Drupal 8 development environment setup, built with Vagrant and Ansible.
I need a simple and straightforward way to have a nice and simple dev env for Drupal 8.
When it comes to OS, I love Debian for my LAMP stack, and I want to have all my envs (dev, staging and production) 
as similar as I can.
This is based on Debian Buster X64, Apache, MariaDb, PHP, all the default distribution versions,
I add mailhog, composer, drush, and some tools I like (nano, htop ...). 
If you want to have a really nice and configurable tool, with lot of options, you can see these pages:

- https://www.drupal.org/docs/official_docs/en/_local_development_guide.html
- https://www.drupal.org/docs/develop/local-server-setup
- https://www.drupalvm.com/

If you just want to have Debian Buster, Apache, Mariadb, mailhog and Drupal, you can go further.

BUT: don't use it as is for production servers, you need to configure php, apache mariadb to fit your server,
and of course take all the necessary security precaution. If you use these Ansible rules, your server will work,
but you don't have a real SSL cert, or security enhancement. This is to speed up the dev, even staging (if it's not 
public), but be more more careful when it comes to your production environment.
You can of course use this as your base, it's MIT licence, but I am pretty sure that you can find a good 
Ansible playbook for this.

# Prerequisites
- virtualization ready hardware
- virtualbox
- nfs
- vagrant
- git
- a texteditor

# Build your development environment

## Clone this repository
```shell script
git clone https://github.com/nicolas-san/drupal_8_simple_dev_env
```

## Create a vars/main.yml file
```shell script
cd drupal_8_simple_dev_env
cp ansible/vars/main_dist.yml ansible/vars/main.yml
```

## Edit and set your values in ansible/vars/main.yml
```shell script
nano ansible/vars/main.yml
```
```yaml
mariadb_root_pass: 'MakeARealPasswordHere'
project_name: 'MyProject'
database_name:  "my_project"
database_user:  "defaultUser"
```
## You can customize the vagrantfile
If you want you can edit the vagrantfile, you can change the hostname, ip, memory ...
```shell script
    config.vm.network "private_network", ip: "192.168.47.11"
    config.vm.hostname = "drupal.localdev"
    v.name = "drupal_8_simple_dev_env"
    v.memory = "2048"
    v.cpus = 2
```

## Run
In the project root dir (drupal_8_simple_dev_env)
```shell script
vagrant up
```
If at some point something is wrong, you can run the provision again with
```shell script
vagrant up --provision
```
Or, destroy and start again
```shell script
vagrant destroy
vagrant up
```

## Install Drupal 8
Go to https://drupal.localdev and install it.

## Mailhog
http://mail.drupal.localdev/

## Debug
You can make ansible more verbose by adding "vv" to the ansible command in the Vagrantfile:
```shell script
ansible.verbose = "vvv"
```

## Thanks
I have read, search and take information and code snippets from lot of places, like stackoverflow, 
and some github repositories.
At have started this only for me, I did not record all the sources, but I want to share, so if you recognize a part of something you share,
 first thank you, and if you want open an issue with your link, or PR this readme, I will add you here :)
- Composer install, thanks to: https://github.com/Vinelab/ansible-composer 

## Licence
Copyright © 03/2020, Bouteillier Nicolas (Kaizendo.fr)
Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

