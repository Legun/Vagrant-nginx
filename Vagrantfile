# -*- mode: ruby -*-
# vi: set ft=ruby :


Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/xenial64"


  config.vm.network "private_network", ip: "192.168.33.11"


  config.vm.synced_folder "./HTML", "/var/www/html"


   config.vm.provision "shell", run: "once" do |package|
	package.inline = "apt-get update; apt-get install docker docker.io -y"

   end

   config.vm.provision "shell" do |firewall|
	firewall.inline = "iptables -A INPUT -p tcp -m tcp --dport 80 -j ACCEPT"
    end

   config.vm.provision "docker", run: "once" do |d|
    d.pull_images "threew82/nginx"

    end
   
   config.vm.provision "docker", run: "always" do |web|
	web.run "threew82/nginx",
		args: "-d -v /var/www/html:/var/www/html -p 80:80 --name nginx"
	end
   
end
