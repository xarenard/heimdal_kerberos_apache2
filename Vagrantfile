# -*- mode: ruby -*-
# vi: set ft=ruby :
#ENV["VAGRANT_DETECTED_OS"] = ENV["VAGRANT_DETECTED_OS"].to_s + " cygwin"

  boxes = [
    { base:"ubuntu/trusty64", name:"kdc.exaple.xa", forwarded_port:9080},
    { base:"ubuntu/trusty64", name:"service.example.xa", forwarded_port:9180}
  ]

Vagrant.configure(2) do |config|
  boxes.each do |boxe|
    config.vm.define boxe[:name] do |b|
        b.vm.box = boxe[:base]
        b.vm.network "forwarded_port",guest: 80,host:boxe[:forwarded_port]
        b.vm.hostname = boxe[:name]
        b.vm.provider "virtualbox" do |v|
            v.customize ["modifyvm", :id, "--cpus","1"]
            v.customize ["modifyvm", :id, "--memory","1024"]
        end
        #b.gui = false

        #provisioning with ansible
        b.vm.provision "ansible" do |ansible|
            ansible.playbook = "../site.yml"
            ansible.inventory_path = "../inventories/vagrant/hosts"
            ansible.sudo = true
            ansible.host_key_checking = false
            ansible.extra_vars = { ansible_ssh_user: 'vagrant'}
            ansible.verbose = ""
        end
    end
  end
end
