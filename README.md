# ansible-mastodon

1. Install ansible.  
   see http://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html

1. Add remote host configuration to `ansible/inventories/hosts.yml`
   see http://docs.ansible.com/ansible/devel/user_guide/intro_inventory.html for more details.
1. After replace `HOST_NAME`, `DOMAIN_NAME`, `PASSWORD` and `EMAIL`, then execute following commands.  
    `HOST_NAME`: target of ansible  
    `DOMAIN_NAME`: use for Let's Encrypt & nginx config  
    `EMAIL`: use for Let's Encrypt  
    `PASSWORD`: use for postgresql db
   
    ```sh
    cd ansible
    ansible-playbook playbooks/mastodon-setup.yml -l HOST_NAME --extra-vars '{ "domain_name":"DOMAIN_NAME", "postgresql_user_password": "PASSWORD", "email": "EMAIL" }'
    ```

    You can use more extra-vars.
    
    | variable | value | |
    |---|---|---|
    | enable_swap | True / False | use swap if remote host has low memory.  (default: False) |
    | stage | "local" / "production" |  If the stage is "local", create not a Let's Encrypt certificate but a self-signed certificate.  (default: "production") |
    | skip_letsencrypt | True / False | If you want to obtain certificate manually, set it True.  (default: False) |
    
    ex) 
    ```
    ansible-playbook playbooks/mastodon-setup.yml -l HOST_NAME --extra-vars '{ "domain_name":"DOMAIN_NAME", "postgresql_user_password": "PASSWORD", "email": "EMAIL", "enable_swap": True, "stage": "local", "skip_letsencrypt": True }'
    ```
    
1. Login remote host via ssh then execute following commands as mastodon user.

    ```sh
    cd ~/live
    RAILS_ENV=production bundle exec rake mastodon:setup
    ```
1. Start mastodon services as root user.

    ```sh
    systemctl start mastodon-{web,sidekiq,streaming}
    ```

    See also https://github.com/tootsuite/documentation/blob/master/Running-Mastodon/Production-guide.md
