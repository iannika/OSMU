# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |server|
  server.vm.box = "ubuntu/trusty64"
  server.vm.box_check_update = false



  server.vm.define "vm1" do |vm1|
      vm1.vm.hostname = "vm1"  
      vm1.vm.network  "public_network", ip: "192.168.1.60", hostname: true
      #server.vm.network "forwarded_port", guest: 80, host: 8080
      
      vm1.vm.provider "virtualbox" do |vb|
         #vb.memory = "1024"
         vb.gui = true
         vb.memory = "1024"
         vb.cpus = 2
      end
  end

  
 server.vm.define "vm2" do |vm2|
     vm2.vm.hostname = "vm2"  
     vm2.vm.network "public_network", ip: "192.168.1.61", hostname: true
     #vm2.vm.network "forwarded_port", guest: 80, host: 8081

     
     vm2.vm.provider "virtualbox" do |vb|
       vb.gui = true
       vb.memory = 1024
       vb.cpus = 2
     end
     
 end


 server.vm.define "vm3" do |vm3|
     vm3.vm.hostname = "vm3"  
     vm3.vm.network "public_network", ip: "192.168.1.62", hostname: true
     #vm3.vm.network "forwarded_port", guest: 80, host: 8081

     
     vm3.vm.provider "virtualbox" do |vb|
       vb.gui = true
       vb.memory = 1024
       vb.cpus = 2
     end
     
  end
 
	



  config.vm.provision "shell" do |s|
    ssh_pub_key = File.readlines("#{Dir.home}/.ssh/id_rsa.pub").first.strip
    s.inline = <<-SHELL
      echo #{ssh_pub_key} >> /home/vagrant/.ssh/authorized_keys
      echo #{ssh_pub_key} >> /root/.ssh/authorized_keys
    SHELL
  end

end
