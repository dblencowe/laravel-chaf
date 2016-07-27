# Laravel CHAF - CHuck up And Forget
This anisble configuration is designed to provide a simple easy to manage way of installing a laravel application on a virtual server.

By default it sets up unattended security upgrades, sets SSH to use key based authentication and creates a deploy user for your app.

## Getting Started
* [Install Ansible](http://docs.ansible.com/ansible/intro_installation.html)
* Clone the repository
* Configure the variables (described below)
* Add your server IP to the inventory file
* Run `ansible-playbook -i inventory playbook.yml`

## Variable files
Variables are located in the vars/ folder and are split in to different sections of the deploy

### apache.yml
* webmaster: The webmaster email you want apache to be configured with
* server_name: The primary domain for your application
* server_alias: A list of aliases you want your app to have. Ex: `*.example.com www.example2.com`

### laravel.yml
* db_name: Database name for your application
* db_user: Database username for your application
* app_env: Laravel application environment to use (`production`, `development`, etc),
* app_debug: Whether to enable laravel debug mode (`true` or `false`)
* app_key: The app key to use (Generate this with `php artisan key:generate`)
* app_url: The primary application url

### php.yml
* version: Version of PHP you want to install (`5.5`, `5.6`, `7.0`)

### repository.yml
* url: Git repository to deploy
* branch: Git branch to deploy

**As well as configuring these two variables you need to put an ssh keypair in roles/repository_pull/files called id_rsa_deployment and id_rsa_deployment.pub. These should be read only keys for your git repository**

### setup.yml
* ssh_key: The path to the public SSH key you want to use to login to the server. Ex: `/Users/dblencowe/.ssh/id_rsa.pub`
* timezone: The timezone you want the server to use. Ex: `Europe/London`


## MySQL access
The config generates random mysql passwords for the root and app accounts. The passwords are stored in /root/.my.cnf and /home/deploy/.my.cnf respectively