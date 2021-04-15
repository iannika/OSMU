# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.box_check_update = false


  config.vm.define "vm1" do |vm1|
      dev.vm.network  "public_network", ip: "192.168.1.60"
      dev.vm.hostname = "vm1"  
      dev.vm.provider "virtualbox" do |vb|
         vb.memory = "4096"
      end
  end

  
 config.vm.define "vm2" do |vm2|
     db.vm.network "public_network", ip: "192.168.1.61"
     db.vm.hostname = "vm2"  
     db.vm.provider "virtualbox" do |vb|
         vb.memory = "1024"
     end
 end


 config.vm.provider "virtualbox" do |vb|
     vb.gui = true
     vb.memory = 1024
     vb.cpus = 2
 end

  

 box.vm.provision "shell", inline: <<-SHELL
     #3
        mkdir -p ~root/.ssh
        cp ~vagrant/.ssh/auth* ~root/.ssh
        yum install -y mdadm smartmontools hdparm gdisk

     #4
	mkdir -p ~root/.ssh
        cp ~vagrant/.ssh/auth* ~root/.ssh      
        yum install -y mdadm smartmontools hdparm gdisk
        cd /home/vagrant && bash ./script.sh
        mdadm --create --verbose /dev/md0 --level=5 --raid-devices=3 /dev/sdb1 /dev/sdc1 /dev/sdd1
        mkdir /etc/mdadm && touch /etc/mdadm/mdadm.conf
        echo "DEVICE partitions" > /etc/mdadm/mdadm.conf
        mdadm --detail --scan --verbose | awk '/ARRAY/ {print}' >> /etc/mdadm/mdadm.conf
        mkfs.ext4 /dev/md0
        mount /dev/md0 /mnt
 SHELL

end
