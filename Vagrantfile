# Install required plugins
required_plugins = ["vagrant-hostsupdater"]
required_plugins.each do |plugin|
    exec "vagrant plugin install #{plugin}" unless Vagrant.has_plugin? plugin
end

Vagrant.configure("2") do |config|
    config.vm.box = "ubuntu/xenial64"
    config.vm.network "private_network", ip: "192.168.10.150"
    config.hostsupdater.aliases = ["database.local"]
    #creates connection for the synced folders betwwen host and vm
    config.vm.synced_folder "environment/db", "/home/ubuntu/environment"

    config.vm.provision "ansible" do |ansible|
      ansible.verbose = "v"
      ansible.playbook = "environment/db/mongo_playbook.yml"
  end
end
