# -*- mode: ruby -*-
# vi: set ft=ruby :

$script = <<-SCRIPT
case "$SUDO_USER" in
  ubuntu )
    apt-get update
    apt-get install -y python
    ;;
  * )
    echo "SUDO_USER: $SUDO_USER"
  ;;
esac
echo "done"
SCRIPT

Vagrant.configure("2") do |config|
  config.vbguest.no_remote = true
  config.vbguest.auto_update = false

  config.vm.define 'trusty' do |instance|
    instance.vm.box = 'ubuntu/trusty64'
  end

  config.vm.define 'xenial' do |instance|
    instance.vm.box = 'ubuntu/xenial64'
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
