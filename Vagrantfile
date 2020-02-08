# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.define "linux" do |config|
    config.vm.box = "centos/7"

    config.vm.provision 'ansible' do |ansible|
      ansible.playbook = 'test.yml'
      ansible.verbose = true
    end
  end

  config.vm.define "freebsd" do |config|
    config.vm.box = "freebsd/FreeBSD-12.1-STABLE"
    config.ssh.shell = '/bin/sh'
    config.vm.provision "shell", inline: <<-SHELL
      pkg update
      pkg upgrade -y
      pkg install -y python
    SHELL

    config.vm.provision 'ansible' do |ansible|
      ansible.playbook = 'test.yml'
      ansible.verbose = true
      ansible.raw_arguments = '-e ansible_python_interpreter=/usr/local/bin/python'
    end
  end

end
