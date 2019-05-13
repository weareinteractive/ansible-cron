# -*- mode: ruby -*-
# vi: set ft=ruby :

$script = <<-SCRIPT
if [ -x "$(command -v apt-get)" ]; then
  apt-get update
  apt-get install -y python
elif [ -x "$(command -v yum)" ]; then
  // yum install ...
else
  // printenv
fi
echo "done"
SCRIPT

Vagrant.configure("2") do |config|
  config.vbguest.no_remote = true
  config.vbguest.auto_update = false

  config.vm.define 'bionic' do |instance|
    instance.vm.box = 'ubuntu/bionic64'
  end

  config.vm.define 'xenial' do |instance|
    instance.vm.box = 'ubuntu/xenial64'
  end

  config.vm.define 'trusty' do |instance|
    instance.vm.box = 'ubuntu/trusty64'
  end

  config.vm.define 'centos7' do |instance|
    instance.vm.box = 'centos/7'
  end

  # install dependencies
  config.vm.provision "shell", inline: $script

  # run ansible
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "tests/main.yml"
    ansible.verbose = 'vv'
    ansible.become = true
  end
end
