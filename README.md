# ansible-mastodon

1. Install ansible
1. Add your server configuration to `ansible/inventories/hosts.yml`  
   see http://docs.ansible.com/ansible/devel/user_guide/intro_inventory.html for more details 

1. After replace `HOST_NAME`, `DOMAIN_NAME`, `PASSWORD` and `EMAIL`, then Execute following commands.
    * `HOST_NAME`: target of ansible
    * `DOMAIN_NAME`: use for Let's Encrypt & nginx config
    * `EMAIL`: use for Let's Encrypt
    * `PASSWORD`: use for postgresql db
   
```
$ cd ansible
$ ansible-playbook playbooks/mastodon-setup.yml -l HOST_NAME --extra-vars '{ "domain_name":"DOMAIN_NAME", "postgresql_user_password": "PASSWORD", "email": "EMAIL" }'
```
