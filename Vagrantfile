VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "debian/bookworm64"
  config.ssh.insert_key = false
  config.vm.synced_folder '.' '/vagrant', disabled: true
  config.vm.provider "virtualbox"

  config.vm.provider :virtualbox do |v|
    v.memory = 2048
    v.cpus = 2
    v.linked_clone = true
  end

  boxes = [
    { :name => "kube-controller-1", :ip => "192.168.56.2" },
    { :name => "kube-worker-1", :ip => "192.168.56.3" },
  ]

  boxes.each_with_index do |opts, index|
    config.vm.define opts[:name] do |config|
      config.vm.hostname = opts[:name]
      config.vm.network :private_network, ip: opts[:ip]
    end
  end

end
