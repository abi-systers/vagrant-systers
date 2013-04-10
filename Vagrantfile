# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant::Config.run do |config|
  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "centos-6-systers-mailman-20130410"
  config.vm.host_name = "systers-dev.systers.org"

  config.vm.box_url = "http://ftp.osuosl.org/pub/osl/vagrant/centos-6-systers-mailman-20130410.box"

  # Boot with a GUI so you can see the screen. (Default is headless)
  # config.vm.boot_mode = :gui

  # config.vm.network :hostonly, "192.168.33.10"

  # Forward a port from the guest to the host, which allows for outside
  # computers to access the VM, whereas host only networking does not.
  config.vm.forward_port 80, 8080
end
