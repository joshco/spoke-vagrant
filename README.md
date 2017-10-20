# Spoke Vagrant

This box will build you an ubuntu vagrant VM with postgres and Spoke dependencies installed.

# Usage

1. Clone this repository into a directory, eg spoke-vagrant

2. Within spoke-vagrant, clone the MoveOn Spoke repository into subdirectory Spoke

3. Customize your .env by using the .env-vagrant that came with this repository

4. run ```vagrant up```
You will see lots of install messages!

5. run ```vagrant ssh``` to log in to the VM

6. ```cd /vagrant/Spoke```

7. ```npm run dev```

8. Point your browser to ```http://192.168.10.10:3000/```

> Note: You'll need to set your Auth0 parameters to actually be able to log in
