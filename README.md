# Spoke Vagrant

This box will build you an ubuntu vagrant VM with postgres and Spoke dependencies installed.

# Usage

1. Clone this repository into a directory, eg spoke-vagrant

2. Within spoke-vagrant, clone the MoveOn Spoke repository into subdirectory Spoke
> It is critical that you clone the Spoke source __before__ you start the VM.  If you don't do this, the provisioning step of VM creation will fail.

3. Customize your .env by using the .env-vagrant that came with this repository

4. run ```vagrant up```
You will see lots of install messages!

5. run ```vagrant ssh``` to log in to the VM

6. ```cd /vagrant/Spoke```

7. ```npm run dev```

8. Point your browser to ```http://192.168.10.10:3000/```

> Note: You'll need to set your Auth0 parameters to actually be able to log in

# Unhosing yourself
If you mess up the system, corrupt the database, or otherwise get to an unworking state, vagrant allows you to destroy and recreate the VM

1. From your shell outside the VM, run `vagrant destroy`
This will shut down the machine and destroy it.
> your source tree will be preserved

2. run `vagrant up`
This will recreate the machine just like the first time.

