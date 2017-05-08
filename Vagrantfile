# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  # hostmanager configs
  config.hostmanager.enabled = true
  config.hostmanager.ignore_private_ip = false
  config.hostmanager.include_offline = true

  # boxes
  config.vm.define 'ansible', primary: true do |ansible|
    config.vm.provider 'virtualbox' do |vb|
      vb.memory = '1024'
      vb.customize ['modifyvm', :id, '--natdnsproxy1', 'off']
      vb.customize ['modifyvm', :id, '--natdnshostresolver1', 'off']
    end
    ansible.vm.box = 'centos/7'
    ansible.vm.hostname = 'ansible.vagrant.box'
    ansible.hostmanager.aliases = %w(ansible)
    ansible.vm.network :private_network, ip: '192.168.250.10'
    ansible.vm.provision :shell, path: 'scripts/ansible.sh'
    ansible.vm.network :forwarded_port, guest: 22, host: 2110, id: 'ssh'
  end

  config.vm.define 'centos' do |centos|
    config.vm.provider 'virtualbox' do |vb|
      vb.memory = '768'
      vb.customize ['modifyvm', :id, '--natdnsproxy1', 'off']
      vb.customize ['modifyvm', :id, '--natdnshostresolver1', 'off']
    end
    centos.vm.box = 'centos/7'
    centos.vm.hostname = 'centos.vagrant.box'
    centos.hostmanager.aliases = %w(centos)
    centos.vm.network :private_network, ip: '192.168.250.11'
    centos.vm.provision :shell, path: 'scripts/centos.sh'
    centos.vm.network :forwarded_port, guest: 22, host: 2111, id: 'ssh'
  end

  config.vm.define 'ubuntu' do |ubuntu|
    config.vm.provider 'virtualbox' do |vb|
      vb.memory = '1024'
      vb.customize ['modifyvm', :id, '--natdnsproxy1', 'off']
      vb.customize ['modifyvm', :id, '--natdnshostresolver1', 'off']
    end
    ubuntu.vm.box = 'ubuntu/trusty64'
    ubuntu.vm.hostname = 'ubuntu.vagrant.box'
    ubuntu.hostmanager.aliases = %w(ubuntu)
    ubuntu.vm.network :private_network, ip: '192.168.250.12'
    ubuntu.vm.provision :shell, path: 'scripts/ubuntu.sh'
    ubuntu.vm.network :forwarded_port, guest: 22, host: 2112, id: 'ssh'
  end
end
