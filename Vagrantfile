# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "debian/bookworm64"
  # config.vbguest.auto_update = false

  config.vm.define "master" do |master|
    master.vm.hostname = "master.deaw.test"
    master.vm.network "private_network", ip: "192.168.57.10"

    master.vm.provision "shell", name: "update", inline: <<-SHELL
      apt-get update
      apt-get install -y bind9
    SHELL
    master.vm.provision "shell", name: "dns-master", inline: <<-SHELL
      cp -v /vagrant/named /etc/default
      cp -v /vagrant/named.conf.options /etc/bind
      cp -v /vagrant/named.conf.local /etc/bind
      cp -v /vagrant/deaw.test.dns /var/lib/bind
      cp -v /vagrant/192.168.57.dns /var/lib/bind
      systemctl reload named
      systemctl status named
    SHELL
  end # master
end