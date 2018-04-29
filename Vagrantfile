# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # download box from vagrant cloud, use ubuntu official
  config.vm.box = "ubuntu/bionic64"

  config.vm.provision :shell, inline: <<-EOF
    sudo apt update && sudo apt install -y python
  EOF

  config.vm.provision :ansible do |ansible|
    ansible.playbook = './playbooks/spinnaker.yml'
    ansible.raw_arguments = ["-v"]
  end
end
