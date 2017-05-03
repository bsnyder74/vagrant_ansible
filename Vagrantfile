# -*- mode: ruby -*-
# vi: set ft=ruby :

# configs
$box_os = 'centos/7'
$ipaddress = '192.168.250.18'
$box_provider = :virtualbox

$setupscript = <<END
  sudo yum install -y epel-release
  sudo yum install -y git python python-devel python-pip openssl ansible
END

Vagrant.configure(2) do |config|
  config.vm.box = $box_os
  config.vm.provider $box_provider do |vb|
    vb.customize ['modifyvm', :id, '--natdnsproxy1', 'off']
    vb.customize ['modifyvm', :id, '--natdnshostresolver1', 'off']
  end

  # boxes
  config.vm.define 'ansible', primary: true do |ansible|
    ansible.vm.hostname = 'ansible'
    ansible.vm.network :private_network, ip: $ipaddress
    ansible.vm.provision :shell, inline: $setupscript
  end

  config.vm.provider $box_provider do |vb|
    vb.memory = '1024'
  end

end
