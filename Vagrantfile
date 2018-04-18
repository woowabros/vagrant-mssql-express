# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = '2'

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.cache.scope = :box if Vagrant.has_plugin?('vagrant-cachier')
  config.vm.box = 'opentable/win-2012r2-standard-amd64-nocm'
  config.vm.network :private_network, ip: '192.168.50.4'
  config.vm.network :forwarded_port, guest: 3389, host: 3389
  config.vm.network :forwarded_port, guest: 1433, host: 1433

  config.vm.provision :shell, path: 'scripts/provision.ps1'

  config.vm.provider 'virtualbox' do |v|
    host = RbConfig::CONFIG['host_os']

    v.destroy_unused_network_interfaces = true
    v.customize [
      'modifyvm', :id,
      '--memory', 2048,
      '--cpus', 2
    ]
  end
end
