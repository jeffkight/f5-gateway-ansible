# -*- mode: ruby -*-
# vi: set ft=ruby :

#
# (c) Copyright 2018 Jeff Kight
#
# Licensed under the Apache License, Version 2.0 (the "License"); you may
# not use this file except in compliance with the License. You may obtain
# a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS, WITHOUT
# WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the
# License for the specific language governing permissions and limitations
# under the License.
#
# Ansible playbook for F5 gateway automation
#
# Author: Jeff Kight <jeff@kight.net>
#

Vagrant.configure("2") do |config|

  config.vm.synced_folder ".", "/vagrant", disabled: true

  config.vm.define "gateway", autostart: true do |gateway|

    gateway.vm.guest = :redhat
    gateway.vm.box = "centos/7"

    # add private gateway for network use -- NAT for public
    gateway.vm.network "private_network", ip: "172.16.145.254", netmask: "255.255.255.0", bridge: "vmnet2"

    gateway.vm.provision :ansible do |ansible|
      ansible.inventory_path = "provisioning/hosts.yml"
      ansible.playbook = "provisioning/site.yml"
      ansible.vault_password_file = ".vaultpass"
    end

  end

end
