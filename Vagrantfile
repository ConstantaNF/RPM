# -*- mode: ruby -*-
# vim: set ft=ruby :
disk_controller = 'IDE'


MACHINES = {
  :rpm => {
        :box_name => "generic/centos8s",
        :box_version => "4.3.12",
        :provision => "install_RPM.sh",
    }
}


Vagrant.configure("2") do |config|


  MACHINES.each do |boxname, boxconfig|


      config.vm.define boxname do |box|


        box.vm.box = boxconfig[:box_name]
        box.vm.box_version = boxconfig[:box_version]
        box.vm.host_name = "rpm"
        box.vm.provider :virtualbox do |vb|
              vb.customize ["modifyvm", :id, "--memory", "1024"]
              needsController = false
        end
        box.vm.provision "shell", path: boxconfig[:provision]
     end

     config.vm.synced_folder "/home/adminkonstantin/RPM/temp", "/srv"
     end
 end
