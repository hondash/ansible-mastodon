# ansible-mastodon

Install ansible  
http://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html


Add remote host configuration to `ansible/inventories/hosts.yml`  
see http://docs.ansible.com/ansible/devel/user_guide/intro_inventory.html for more details 

After replace `HOST_NAME`, `DOMAIN_NAME`, `PASSWORD` and `EMAIL`, then execute following commands.

* `HOST_NAME`: target of ansible
* `DOMAIN_NAME`: use for Let's Encrypt & nginx config
* `EMAIL`: use for Let's Encrypt
* `PASSWORD`: use for postgresql db
   
```sh
cd ansible
ansible-playbook playbooks/mastodon-setup.yml -l HOST_NAME --extra-vars '{ "domain_name":"DOMAIN_NAME", "postgresql_user_password": "PASSWORD", "email": "EMAIL" }'
```

Login remote host via ssh then execute following commands as mastodon user.

```sh
cd ~/live
RAILS_ENV=production bundle exec rake mastodon:setup
```

Start mastodon services.

```sh
systemctl start mastodon-{web,sidekiq,streaming}
```

See also https://github.com/tootsuite/documentation/blob/master/Running-Mastodon/Production-guide.md
