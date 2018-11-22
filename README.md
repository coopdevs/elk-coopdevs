# Tryton Provision

Ansible project to setup a server of log monitoring using the [ELK stack](https://www.elastic.co/elk-stack).

## Requeriments

This project has been thinked to run in Debian 9.0 (Stretch

* Ansible 2.5.2 or last

You can find more information about Ansible [here](http://docs.ansible.com/)

## Playbooks

### Create System Administrators users - `playbooks/sys_admins.yml`

This playybook use the [`sys-admins` role](https://github.com/coopdevs/sys-admins-role) of Coopdevs to manage the system administrators users.

### SetUp ELK server - `playbooks/site.yml`
This playbook do run the next community roles:

* [Geerlingguy Java](https://galaxy.ansible.com/geerlingguy.java)
* [Geerlingguy Elasticsearch](https://galaxy.ansible.com/geerlingguy.elasticsearch)
* [Geerlingguy Logstash](https://galaxy.ansible.com/geerlingguy.logstash)
* [Geerlingguy Kibana](https://galaxy.ansible.com/geerlingguy.kibana)
* [Geerlingguy htpasswd](https://galaxy.ansible.com/geerlingguy.htpasswd)
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

* Basic Auth
```YAML
kibana_admin: "coopdevs"
kibana_password: "1234"
```

## Ansible Community Roles

To download the community roles, you can run:
```
ansible-galaxy install -r requirements.yml
```

### List of Galaxy roles:

* [Geerlingguy Java](https://galaxy.ansible.com/geerlingguy.java)
* [Geerlingguy Elasticsearch](https://galaxy.ansible.com/geerlingguy.elasticsearch)
* [Geerlingguy Logstash](https://galaxy.ansible.com/geerlingguy.logstash)
* [Geerlingguy Kibana](https://galaxy.ansible.com/geerlingguy.kibana)
* [Geerlingguy htpasswd](https://galaxy.ansible.com/geerlingguy.htpasswd)
* [Jdauphant NGINX](https://galaxy.ansible.com/jdauphant.nginx)

## Devenv

We use [`devenv`](https://github.com/coopdevs/devenv) tool to manage the development environment. Check the `.devenv` configuration file.

Install and run `devenv` to start a development environment.

## Contributing

1. Fork it (<https://github.com/coopdevs/tryton_provision>)
2. Create your feature branch (`git checkout -b feature/fooBar`)
3. Commit your changes (`git commit -am 'Add some fooBar'`)
4. Push to the branch (`git push origin feature/fooBar`)
5. Create a new Pull Request


