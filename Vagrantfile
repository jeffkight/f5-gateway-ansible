# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.synced_folder ".", "/vagrant", disabled: true

  config.vm.define "gateway", autostart: true do |gateway|

    gateway.vm.guest = :redhat
    gateway.vm.box = "centos/7"
    # gateway.vm.provider :vmware_desktop do |vmware|
    #   vmware.vmx["ethernet0.pcislotnumber"] = "32"
    # end

    # local static port
    # gateway.vm.network "forwarded_port", guest: 22, host: 2080

    # vmnet8
    gateway.vm.network "private_network", ip: "172.16.145.254", netmask: "255.255.255.0", bridge: "vmnet2"

    gateway.vm.provision :ansible do |ansible|
      ansible.inventory_path = "provisioning/hosts.yml"
      ansible.playbook = "provisioning/site.yml"
      ansible.vault_password_file = ".vaultpass"
    end

  end

end
