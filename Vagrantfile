Vagrant.require_version ">= 1.7.0"


$install_nginx = <<SCRIPT
sudo apt-get update -y
sudo apt-get install nginx -y
SCRIPT

Vagrant.configure(2) do |config|
    config.vm.box = "bento/ubuntu-18.04"

    config.vm.provider "hyperv" do |v|
      v.maxmemory = 4048
      v.memory = 4048
      v.cpus = 2
    end
    config.vm.provision "shell", inline: $install_nginx, run: "always"
end
    