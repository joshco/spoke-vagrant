# Spoke Vagrant

This box will build you an ubuntu vagrant VM with postgres and Spoke dependencies installed.  You'll need to install VirtualBox, and then Vagrant as prerequisites.
> For instructions, see: https://www.vagrantup.com/intro/getting-started/index.html

# Usage

1. Clone this repository into a directory, eg spoke-vagrant

2. Within spoke-vagrant, clone the MoveOn Spoke repository into subdirectory Spoke

   run ```git clone https://github.com/MoveOnOrg/Spoke.git```

> It is critical that you clone the Spoke source __before__ you start the VM.  If you don't do this, the provisioning step of VM creation will fail.

3. Customize your .env by using the .env-vagrant that came with this repository

4. run ```vagrant up```
You will see lots of install messages!

5. run ```vagrant ssh``` to log in to the VM

6. ```cd /vagrant/Spoke```

7. ```npm run dev```

8. Point your browser to ```http://192.168.10.10:3000/```

> Note: You'll need to set your Auth0 parameters to actually be able to log in

# Shutting down the VM
When you are not working on Spoke, you can shut down the VM. When you shut it down, all state is preserved.  So any changes you made to the VM will persist between shutdown/reboot.  Your source tree will also be preserved.

1. run `vagrant halt` to shut down
2. run `vagrant up` to restart

# Unhosing yourself
If you mess up the system, corrupt the database, or otherwise get to an unworking state, vagrant allows you to destroy and recreate the VM

1. From your shell outside the VM, run `vagrant destroy`
This will shut down the machine and destroy it.
> your source tree will be preserved

2. run `vagrant up`
This will recreate the machine just like the first time.

# Vagrant Help

* run `vagrant help` for all commands

* run `vagrant status` to check the status (up/down) of your VM

* run `vagrant ssh` to ssh login to the VM
