# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"

  config.vm.network "public_network", bridge: "en0: Wi-Fi (Wireless)"

  config.vm.provision "shell", inline: <<-SHELL
    yum -y install dnsmasq
    systemctl enable dnsmasq

    cp -f /vagrant/etc/dnsmasq.d/dev.conf /etc/dnsmasq.d/dev.conf

    systemctl start dnsmasq
  SHELL

  config.vm.provision "shell", run: "always", inline: <<-SHELL
    echo "copy /etc/hosts"
    cp -f /vagrant/etc/hosts /etc/hosts
    ip addr show
  SHELL
end
