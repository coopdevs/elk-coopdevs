# ELK Stack Provision

Ansible project to setup a server of log monitoring using the [ELK stack](https://www.elastic.co/elk-stack).

## Requeriments

This project has been thinked to run in Debian 9.0 (Stretch

* Ansible 2.5.2 or last

You can find more information about Ansible [here](http://docs.ansible.com/)

### System Requirements

* Ubuntu Bionic 18.04 LTS
* Java version <= 8

> Logstash doesn't support Java 10, which is available on Bionic from `openjdk-11-jre`. If you have it installed on your system, remove it. Use the older version until Logstash gets support, `openjdk-8-jre`.  

#### Minim hardware
* 2 CPUs
* 8 GB RAM

## Playbooks

### Create System Administrators users - `playbooks/sys_admins.yml`

This playybook use the [`sys-admins` role](https://github.com/coopdevs/sys-admins-role) of Coopdevs to manage the system administrators users.

### SetUp ELK server - `playbooks/site.yml`
This playbook do run the next community roles:

* [Geerlingguy Security](https://galaxy.ansible.com/geerlingguy.security)
* [Geerlingguy Java](https://galaxy.ansible.com/geerlingguy.java)
* [Geerlingguy Elasticsearch](https://galaxy.ansible.com/geerlingguy.elasticsearch)
* [Geerlingguy Logstash](https://galaxy.ansible.com/geerlingguy.logstash)
* [Geerlingguy Kibana](https://galaxy.ansible.com/geerlingguy.kibana)
* [Geerlingguy htpasswd](https://galaxy.ansible.com/geerlingguy.htpasswd)
* [Coopdevs Certbot NGINX](https://galaxy.ansible.com/coopdevs.certbot_nginx)
* [Jdauphant NGINX](https://galaxy.ansible.com/jdauphant.nginx)

To use, run:
```
ansible-playbook playbooks/site.yml --limit HOSTGROUP <--tags TAGS -v>
```

## Configurable Variables

This examples are from `./inventory/host_vars/local.tryton.coop/config.yml`. You can create new `host_vars` folder with your domain as name and modify this vars.
We recommend encrypting the variables with sensitive information with [Ansible Vualt](https://docs.ansible.com/ansible/2.4/vault.html) and use `--ask-vault-pass` in the command line.

* Sysadmins
```YAML
system_administrators_group:      # System administrators group
system_administrators:            # List of system administrators added to the group
  - name:                         # User name
    ssh_key:                      # User SSH public key file path
    state:                        # User state (present/absent)
```

* NGINX, BAuth, Certbot
```YAML
development_environment:          # Set 'development_environment' to "true" to skip SSL and nginx tasks
```

* LetsEncrypt
```YAML
certificate_authority_email:      # Let's Encrypt configuration email
```

* Basic Auth
```YAML
kibana_admin:                     # Basic Authentication user
kibana_password:                  # Basic Authentication password
```

## Ansible Community Roles

To download the community roles, you can run:
```
ansible-galaxy install -r requirements.yml
```

### List of Galaxy roles:

* [Coopdevs SysAdmins](https://galaxy.ansible.com/coopdevs.sys-admins-role)
* [Geerlingguy Security](https://galaxy.ansible.com/geerlingguy.security)
* [Geerlingguy Java](https://galaxy.ansible.com/geerlingguy.java)
* [Geerlingguy Elasticsearch](https://galaxy.ansible.com/geerlingguy.elasticsearch)
* [Geerlingguy Logstash](https://galaxy.ansible.com/geerlingguy.logstash)
* [Geerlingguy Kibana](https://galaxy.ansible.com/geerlingguy.kibana)
* [Geerlingguy htpasswd](https://galaxy.ansible.com/geerlingguy.htpasswd)
* [Coopdevs Certbot NGINX](https://galaxy.ansible.com/coopdevs.certbot_nginx)
* [Jdauphant NGINX](https://galaxy.ansible.com/jdauphant.nginx)

## Devenv

We use [`devenv`](https://github.com/coopdevs/devenv) tool to manage the development environment. Check the `.devenv` configuration file.

Install and run `devenv` to start a development environment.

> :warning: **Ubuntu Bionic (18.04) needs install `gpg` package first of all.** :warning:

> To allow to add new ppa repositories. You can run:
> ```
> lxc-attach -n <container-name> -- apt install gpg
> ```

## Contributing

1. Fork it (<https://github.com/coopdevs/elk-coopdevs>)
2. Create your feature branch (`git checkout -b feature/fooBar`)
3. Commit your changes (`git commit -am 'Add some fooBar'`)
4. Push to the branch (`git push origin feature/fooBar`)
5. Create a new Pull Request


