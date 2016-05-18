Vagrant.require_version ">= 1.7.0"


Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/trusty64"

  config.vm.provision "ansible" do |ansible|
    ansible.verbose = "v"
    ansible.playbook = "playbook.yml"
  end


  config.vm.define "rabbitmq-01" do |node|
    node.vm.hostname = "rabbitmq-01"
    node.vm.network "private_network", ip: "192.168.123.100"
  end

  config.vm.define "rabbitmq-02" do |node|
    node.vm.hostname = "rabbitmq-02"
    node.vm.network "private_network", ip: "192.168.123.101"
  end

  config.vm.provider "virtualbox"
end
