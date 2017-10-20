# -*- mode: ruby -*-
# vi: set ft=ruby :
# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|

  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "ubuntu/trusty64"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  config.vm.network "forwarded_port", guest: 3000, host: 3100

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network "private_network", ip: "192.168.10.10"


  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder ".", "/vagrant", type: "rsync",
  #   rsync__auto: true,
  #   rsync__exclude: ".git/",
  #   id: "shared-folder-id",
  #   working_directory: "c:/users/josh/dev/vag/vb2/",
  #   rsync__verbose: true
    
  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  config.vm.provider "virtualbox" do |vb|
    # Display the VirtualBox GUI when booting the machine
    # vb.gui = true
    #   # Customize the amount of memory on the VM:
    vb.memory = "3500"
    vb.cpus="1"
    vb.customize ["guestproperty", "set", :id, "/VirtualBox/GuestAdd/VBoxService/--timesync-set-threshold", 10000]
    vb.customize ["setextradata", :id, "VBoxInternal2/SharedFoldersEnableSymlinksCreate/v-root", "1"]
  end
    
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Define a Vagrant Push strategy for pushing to Atlas. Other push strategies
  # such as FTP and Heroku are also available. See the documentation at
  # https://docs.vagrantup.com/v2/push/atlas.html for more information.
  # config.push.define "atlas" do |push|
  #   push.app = "YOUR_ATLAS_USERNAME/YOUR_APPLICATION_NAME"
  # end

$script = <<SCRIPT
sudo apt-get update
sudo apt-get install -y sqlite postgresql postgresql-contrib

echo "Switching to postgres"

sudo -u postgres /vagrant/pgsetup.sh

mkdir /home/vagrant/spoke_node_modules
chown vagrant /home/vagrant/spoke_node_modules

SCRIPT

$user_script=<<USER
id -a

cd /home/vagrant

curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.5/install.sh | bash
source ~/.bashrc
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion

echo "Installing Node"
nvm install node

cd /vagrant/Spoke
echo "Running npm install for Spoke!"
npm install
npm install -g foreman


USER

$post_boot=<<BOOT
echo "Bind mount node_modules"
mount --bind /home/vagrant/spoke_node_modules /vagrant/Spoke/node_modules

BOOT

  config.vm.provision "fix-no-tty", type: "shell", run: 'always' do |s|
      s.privileged = false
      s.inline = "sudo sed -i '/tty/!s/mesg n/tty -s \\&\\& mesg n/' /root/.profile"
  end

  config.vm.provision "shell", inline: $script
  config.vm.provision :shell, inline: $post_boot, run: 'always'
  config.vm.provision "shell", privileged: false, inline: $user_script
  

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   sudo apt-get update
  #   sudo apt-get install -y apache2
  # SHELL
end
