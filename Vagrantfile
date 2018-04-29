# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.define "spinnaker", primary: true do |spinnaker|
    spinnaker.vm.box = "ubuntu/xenial64"

    spinnaker.ssh.pty = false
    spinnaker.ssh.shell = "bash -c 'BASH_ENV=/etc/profile exec bash'"

    spinnaker.vm.network "private_network", ip: "192.168.33.10"
    spinnaker.vm.provision :shell, inline: <<-EOF
      sudo apt-get update
      sudo apt-get install -y python
      wget https://bootstrap.pypa.io/get-pip.py
      python get-pip.py
    EOF

    spinnaker.vm.provision :ansible do |ansible|
      ansible.playbook = './playbooks/spinnaker.yml'
      ansible.raw_arguments = ["-v"]
    end
  end
end
