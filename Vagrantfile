# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure("2") do |config|
  #
  config.vm.box = "centos/8"

  config.ssh.insert_key = false

  config.vm.synced_folder ".", "/vagrant", disabled: true

  config.vm.provider:virtualbox do |v|
    v.memory = 512
    v.linked_clone = true
  end

  config.vm.define "app1" do |app|
    app.vm.hostname = "app1.test"
    app.vm.network:private_network, ip: "192.168.60.4"
    app.vm.provision "ansible" do |ansible|
        ansible.playbook = "app_playbook.yml"
        ansible.inventory_path = "inventory.ini"
        ansible.limit = "app"
    end
  end

  config.vm.define "db" do |db|
    db.vm.hostname = "db.test"
    db.vm.network:private_network, ip: "192.168.60.6"
    db.vm.provision "ansible" do |ansible|
        ansible.playbook = "db_playbook.yml"
        ansible.inventory_path = "inventory.ini"
        ansible.limit = "db"
    end
  end

end
