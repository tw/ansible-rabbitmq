Vagrant.require_version ">= 1.7.0"


Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/trusty64"

  config.vm.define "rabbitmq-01" do |node|
    node.vm.hostname = "rabbitmq-01"
    node.vm.network "private_network", ip: "192.168.123.100"
    node.vm.provision "shell", inline: "echo '192.168.123.101 rabbitmq-02' | sudo tee --append /etc/hosts"

    ansible_provision node
  end

  config.vm.define "rabbitmq-02" do |node|
    node.vm.hostname = "rabbitmq-02"
    node.vm.network "private_network", ip: "192.168.123.101"
    node.vm.provision "shell", inline: "echo '192.168.123.100 rabbitmq-01' | sudo tee --append /etc/hosts"

    ansible_provision node
  end

  # workaround for ordering of provisioners, we need the hosts to be updated first
  def ansible_provision c
    c.vm.provision "ansible" do |ansible|
      ansible.verbose = "v"
      ansible.playbook = "playbook.yml"
    end
  end

  config.vm.provider "virtualbox"
end
