# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

# Special Settings for this Vagrant Environment
USE_PUBLIC_NETWORK = false
#USE_PUBLIC_NETWORK = true
PRIVATE_NETWORK_BASE = "192.168.1"
#PRIVATE_NETWORK_BASE = PRIVATE_NETWORK_BASE + ""
PUBLIC_NETWORK_BASE = "137.193.211"
#PUBLIC_NETWORK_BASE = "192.168.2"
AUTOSTART_SECONDARY = false
#AUTOSTART_SECONDARY = true
AUTOSTART_INFRASTRUKTURE = false
#AUTOSTART_INFRASTRUKTURE = true

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "ubuntu/trusty64"
  #config.vm.box = "ubuntu/xenial64"

  config.ssh.forward_agent = true

  config.vm.define "ansiblem1.verwaltung.uni-muenchen.de", primary: true, autostart: true do |node|
    node.vm.box = "ubuntu/trusty64"
    node.vm.provider "virtualbox" do |vb|
      vb.name = "NodeMaster1"
      vb.memory = 4096
      vb.cpus = 4
      vb.customize ["modifyvm", :id,
                    "--cpuexecutioncap", "50",
                    "--groups", "/Vagrant/LMU/NodeMaster"
                   ]
    end

    #node.vm.network "forwarded_port", guest: 3000, host: 8000
    #node.vm.network "forwarded_port", guest: 3001, host: 8001
    #node.vm.network "forwarded_port", guest: 5000, host: 5000
    #node.vm.network "forwarded_port", guest: 5432, host: 5432
    #node.vm.network "forwarded_port", guest: 9001, host: 9001

    if ENV['OS'] != "Windows_NT"
      node.vm.network :private_network, ip: PRIVATE_NETWORK_BASE + ".10"
      if USE_PUBLIC_NETWORK
        node.vm.network :public_network, ip: PUBLIC_NETWORK_BASE + ".10"
      end
    end
    if ENV['OS'] == "Windows_NT"
      node.vm.network "forwarded_port", guest: 80, host: 80
      node.vm.network "forwarded_port", guest: 443, host: 443
    end
  end

  config.vm.define "ansiblem2.verwaltung.uni-muenchen.de", autostart: false do |node|
    node.vm.box = "ubuntu/xenial64"
    node.vm.provider "virtualbox" do |vb|
      vb.name = "NodeMaster2"
      vb.memory = 4096
      vb.cpus = 4
      vb.customize ["modifyvm", :id,
                    "--cpuexecutioncap", "50",
                    "--groups", "/Vagrant/LMU/NodeMaster"
                   ]
    end

    #node.vm.network "forwarded_port", guest: 3000, host: 8000
    #node.vm.network "forwarded_port", guest: 3001, host: 8001
    #node.vm.network "forwarded_port", guest: 5000, host: 5000
    #node.vm.network "forwarded_port", guest: 5432, host: 5432
    #node.vm.network "forwarded_port", guest: 9001, host: 9001

    if ENV['OS'] != "Windows_NT"
      node.vm.network :private_network, ip: PRIVATE_NETWORK_BASE + ".11"
      if USE_PUBLIC_NETWORK
        node.vm.network :public_network, ip: PUBLIC_NETWORK_BASE + ".11"
      end
    end
    if ENV['OS'] == "Windows_NT"
      node.vm.network "forwarded_port", guest: 80, host: 80
      node.vm.network "forwarded_port", guest: 443, host: 443
    end
  end

  config.vm.define "ansiblem3.verwaltung.uni-muenchen.de", autostart: false do |node|
    node.vm.box = "debian/jessie64"
    node.vm.provider "virtualbox" do |vb|
      vb.name = "NodeMaster3"
      vb.memory = 4096
      vb.cpus = 4
      vb.customize ["modifyvm", :id,
                    "--cpuexecutioncap", "50",
                    "--groups", "/Vagrant/LMU/NodeMaster"
                   ]
    end

    #node.vm.network "forwarded_port", guest: 3000, host: 8000
    #node.vm.network "forwarded_port", guest: 3001, host: 8001
    #node.vm.network "forwarded_port", guest: 5000, host: 5000
    #node.vm.network "forwarded_port", guest: 5432, host: 5432
    #node.vm.network "forwarded_port", guest: 9001, host: 9001

    if ENV['OS'] != "Windows_NT"
      node.vm.network :private_network, ip: PRIVATE_NETWORK_BASE + ".12"
      if USE_PUBLIC_NETWORK
        node.vm.network :public_network, ip: PUBLIC_NETWORK_BASE + ".12"
      end
    end
    if ENV['OS'] == "Windows_NT"
      node.vm.network "forwarded_port", guest: 80, host: 80
      node.vm.network "forwarded_port", guest: 443, host: 443
    end
  end

  config.vm.define "ansiblem4.verwaltung.uni-muenchen.de", autostart: false do |node|
    node.vm.box = "centos/7"
    node.vm.provider "virtualbox" do |vb|
      vb.name = "NodeMaster4"
      vb.memory = 4096
      vb.cpus = 4
      vb.customize ["modifyvm", :id,
                    "--cpuexecutioncap", "50",
                    "--groups", "/Vagrant/LMU/NodeMaster"
                   ]
    end

    #node.vm.network "forwarded_port", guest: 3000, host: 8000
    #node.vm.network "forwarded_port", guest: 3001, host: 8001
    #node.vm.network "forwarded_port", guest: 5000, host: 5000
    #node.vm.network "forwarded_port", guest: 5432, host: 5432
    #node.vm.network "forwarded_port", guest: 9001, host: 9001

    if ENV['OS'] != "Windows_NT"
      node.vm.network :private_network, ip: PRIVATE_NETWORK_BASE + ".13"
      if USE_PUBLIC_NETWORK
        node.vm.network :public_network, ip: PUBLIC_NETWORK_BASE + ".13"
      end
    end
    if ENV['OS'] == "Windows_NT"
      node.vm.network "forwarded_port", guest: 80, host: 80
      node.vm.network "forwarded_port", guest: 443, host: 443
    end
  end

  if ENV['OS'] != "Windows_NT"
    config.vm.provision "ansible" do |ansible|
      #ansible.playbook = "lmu.ansible.playbooks/base-preseed.yml"
      ansible.playbook = "lmu.ansible.playbooks/nodemaster.yml"
      ansible.groups = {
        "nodemasters" => ["ansiblem1.verwaltung.uni-muenchen.de",
                          "ansiblem2.verwaltung.uni-muenchen.de",
                          "ansiblem3.verwaltung.uni-muenchen.de",
                         ]
      }
      #ansible.verbose = "vvvv"
      #ansible.verbose = "vvv"
      #ansible.verbose = "vv"
      ansible.verbose = "v"
      #ansible.verbose = ""
      #ansible.start_at_task = "Ensure TheForeman Repository Key is present"
      ansible.limit = "all"
      #ansible.limit = "lmu.ansible.playbooks/nodemaster.retry"
      #ansible.tags = ["setup", "configuration", "update"]
      #ansible.skip_tags = ["update"]
      #ansible.ask_vault_pass = true
    end
  elsif ENV['OS'] == "Windows_NT"
    config.vm.provision "ansible_local" do |ansible|
      ansible.version = "latest"
      ansible.install = true
      #ansible.provisioning_path = "/vagrant/"
      #ansible.inventory_path = "nodemaster_ansible_local.inventory"
      #ansible.playbook = "lmu.ansible.playbooks/base-preseed.yml"
      ansible.playbook = "lmu.ansible.playbooks/nodemaster.yml"
      ansible.groups = {
        "nodemasters" => ["ansiblem1.verwaltung.uni-muenchen.de", ]
      }
      #ansible.verbose = "vvvv"
      #ansible.verbose = "vvv"
      #ansible.verbose = "vv"
      #ansible.verbose = "v"
      #ansible.verbose = ""
      #ansible.start_at_task = "Start Setup Instance"
      #ansible.start_at_task = "Setup Redmine Multi-Instance"
      ansible.limit = "all"
      #ansible.limit = "lmu.ansible.playbooks/redmine.retry"
      #ansible.tags = ["setup", "configuration", "update"]
      #ansible.skip_tags = ["update"]
      #ansible.ask_vault_pass = true
    end
  end
end
