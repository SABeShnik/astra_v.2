nodes = [
#	{ :hostname => 'vm1', :ip => '10.245.1.202', :memory => 3076, :cpu => 2, :boxname => "ubuntu/trusty64" },
  { :hostname => 'exporter', :memory => 2048, :cpu => 4, :boxname => "ubuntu/focal64" },

]

Vagrant.configure("2") do |config|
  nodes.each do |node|
      config.vm.box_check_update = false
      config.vm.network "forwarded_port", guest: 3000, host: 3000
      config.vm.define node[:hostname] do |nodeconfig|
          nodeconfig.vm.box = node[:boxname]
          nodeconfig.vm.hostname = node[:hostname]
#          nodeconfig.vm.network :private_network, ip: node[:ip]
          nodeconfig.vm.provider :virtualbox do |vb|
            vb.memory = node[:memory]
            vb.cpus = node[:cpu]
          end
        end
  end

  config.vm.provision "ansible" do |ansible|
     ansible.playbook = "playbook_Node_Exporter_Grafana_Prometheus.yml"
  end


end
#vagrant ssh -- -L 3000:localhost:3000
