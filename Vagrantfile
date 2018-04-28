# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  #-----------------------------------------------------------------------------
  # Common
  #-----------------------------------------------------------------------------
  config.ssh.insert_key = false

  config.vm.provision(:ansible_local) do |ansible|
    ansible.install_mode = "pip"
    ansible.version = "2.5.2"
    ansible.compatibility_mode = "2.0"
    ansible.become = true
    ansible.become_user = "root"
    ansible.playbook = "ansible/playbooks/mastodon-setup.yml"
    ansible.config_file = "ansible/ansible.cfg"
    ansible.groups = {
      "test" => ["centos", "debian", "ubuntu"],
      "test:vars" => {
        "enable_swap": true,
        "domain_name": "localhost",
        "email": "admin@example.com",
        "stage": "local",
        "skip_letsencrypt": false,
        "postgresql_user_password": "test_password"
      }
    }
    #ansible.verbose = "-vvv"
  end

  config.vm.provider(:virtualbox) do |vb|
    vb.gui = false
    vb.cpus = 1
    vb.memory = "512"
  end

  #-----------------------------------------------------------------------------
  # CentOS 7
  #-----------------------------------------------------------------------------
  config.vm.define(:centos, primary: true) do |centos|
    centos.vm.hostname = "centos"
    centos.vm.box = "centos/7"
    centos.vm.box_version = "1801.02"
    centos.vm.network "private_network", ip: "192.168.99.10"
  end

  #-----------------------------------------------------------------------------
  # Debian
  #-----------------------------------------------------------------------------
  config.vm.define(:debian, primary: true) do |debian|
    debian.vm.hostname = "debian"
    debian.vm.box = "debian/stretch64"
    debian.vm.box_version = "9.3.0"
    debian.vm.network "private_network", ip: "192.168.99.20"
  end

  #-----------------------------------------------------------------------------
  # Ubuntu
  #-----------------------------------------------------------------------------
  config.vm.define(:ubuntu, primary: true) do |ubuntu|
    ubuntu.vm.hostname = "ubuntu"
    ubuntu.vm.box = "ubuntu/xenial64"
    ubuntu.vm.box_version = "20180309.0.0"
    ubuntu.vm.network "private_network", ip: "192.168.99.30"
  end

end
