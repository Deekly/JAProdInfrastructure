Vagrant.configure("2") do |config|					# define actual configuration version
    servers=[										# define an array of three VMs each with own parameters which I want to create
        {
          :hostname => "control",
          :box => "bento/ubuntu-18.04",
          :ip => "192.168.34.10",
          :ssh_port => '2200'
        },
        {
          :hostname => "node1",
          :box => "bento/ubuntu-18.04",
          :ip => "192.168.34.11",
          :ssh_port => '2201'
        },
        {
          :hostname => "node2",
          :box => "bento/ubuntu-18.04",
          :ip => "192.168.34.12",
          :ssh_port => '2202'
        }
      ]

    servers.each do |machine|						 # 
        config.vm.define machine[:hostname] do |node|
            node.vm.box = machine[:box]
            node.vm.hostname = machine[:hostname]
            node.vm.network :private_network, ip: machine[:ip]
            node.vm.network "forwarded_port", guest: 22, host: machine[:ssh_port], id: "ssh"
            node.vm.provider :virtualbox do |vb|
                vb.customize ["modifyvm", :id, "--memory", 512]
                vb.customize ["modifyvm", :id, "--cpus", 1]
            end
        end
    end
end