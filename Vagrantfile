# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.provider "virtualbox" do |v|
    v.customize ["modifyvm", :id, "--cpuexecutioncap", "50"]
  end

  config.vm.define "spinnaker", primary: true do |spinnaker|
    spinnaker.vm.provider "virtualbox" do |v|
      v.memory = 4096
      v.cpus = 4
    end

    spinnaker.vm.box = "ubuntu/xenial64"

    spinnaker.ssh.pty = false
    spinnaker.ssh.shell = "bash -c 'BASH_ENV=/etc/profile exec bash'"

    spinnaker.vm.network "private_network", ip: "192.168.33.10"
    spinnaker.vm.provision :shell, inline: <<-EOF
      /usr/bin/env python --version
      if [ "$?" != "0" ]; then
        sudo apt-get update
        sudo apt-get install -y python
      fi

      /usr/bin/env pip --version
      if [ "$?" != "0" ]; then
        wget https://bootstrap.pypa.io/get-pip.py
        python get-pip.py
      fi
    EOF

    spinnaker.vm.provision :ansible do |ansible|
      ansible.playbook = './playbooks/spinnaker.yml'
      ansible.raw_arguments = ["-v"]
    end
  end
end
