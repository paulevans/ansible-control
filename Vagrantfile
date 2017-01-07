# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

    # Ensure we use our vagrant private key
    config.ssh.insert_key = false
    config.ssh.private_key_path = '~/.vagrant.d/insecure_private_key'

    config.vm.define 'anxs' do |machine|
        machine.vm.box = "bento/ubuntu-16.04"

        machine.vm.hostname = 'anxs.local'

        machine.vm.provision 'ansible_local' do |ansible|
            ansible.playbook = 'vagrant-playbook.yml'
            ansible.sudo = true
            ansible.inventory_path = 'vagrant-inventory'
            ansible.host_key_checking = false
        end
    end

    # Provider specific settings.
    config.vm.provider "virtualbox" do |v|
        v.memory = 2048
        v.cpus = 2
    end

    # Create the inventory for the servers just started.
    require "fileutils"
    f = File.open("vagrant-inventory","w")

    f.puts config.vm.anxs.ip_addr

    f.close
end
