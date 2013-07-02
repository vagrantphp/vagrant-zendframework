Vagrant.configure("2") do |config|

	# Operating System
	
	## Ubuntu 12.04 (64-bit)
  config.vm.box = "precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"
    
  # Set the Timezone to something useful
  config.vm.provision :shell, :inline => "echo \"America/Chicago\" | sudo tee /etc/timezone && dpkg-reconfigure --frontend noninteractive tzdata" 
  
  # Setup the synced folder for local development
  config.vm.synced_folder "./www", "/var/www", id: "vagrant-root"
  
  ###
  #  Creates a basic LAMP stack with MySQL
  #  
  #  To launch run: vagrant up lamp
  ###
  config.vm.define :lamp do |lamp_config|
    # Map dev.pyrocms.mysql to this IP
    lamp_config.vm.network :private_network, ip: "192.168.50.4"
    
    lamp_config.ssh.forward_agent = true
       
	  lamp_config.vm.provision :puppet do |puppet|
 
	    puppet.manifests_path = "manifests"
	    puppet.module_path = "modules"
	    puppet.options = ['--verbose']
	  end
	  
	  lamp_config.vm.provision :shell, :inline => "composer create-project -sdev --repository-url='http://packages.zendframework.com' zendframework/skeleton-application /vagrant/www/zendframwork"
	  	  
  end
  
   
  
end
