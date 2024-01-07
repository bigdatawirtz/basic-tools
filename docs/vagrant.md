Vagrant helps you to create and manage a virtualized environment.

## Installing

Vagrant requires a previous VirtualBox installation. 

Download and install Vagrant from: https://www.vagrantup.com/

## Commands

* `vagrant init`: Initialize a Vagranfile.
* `vagrant up`: Create a virtual machine from Vagratfile.
  * `vagrant up --debug`: verbose debug option
* `vagrant ssh`: SSH conection to the current virtual machine.
* `vagrant suspend`: suspends the current machine (save state)
* `vagrant resume`: resume a suspended vagrant machine
* `vagrant halt`: shutdown a virtual machine
* `vagrant destroy`: stops and delete the vagrant machine
* `vagrant provision`: force the provisioners to be run again a virtual machine. Useful for updating the configuration of existing virtual machines. 

## Vagrant first steps tutorial

Instructions to create a ubuntu virtual machine from scratch.

1. Create a directory for your virtual machine configuration: `mkdir my-vm`
2. Move to the new directory: `cd my-vm`
3. Initialize a configuration file: `vagrant init`
4. Edit the new file 'Vagrantfile' deletig all commented lines: `nano Vagrantfile`
```
Vagrant.configure("2") do |config|
  config.vm.box = "base"
end
```
5. Launch a new virtual machine based on the current Vagrantfile: `vagrant up`

The proccess will fail due to a bad configuration. There's no "base" box.

6. Edit the Vagrantfile. Change "base" for another valid box name (view boxes on [Vagrant Cloud](https://app.vagrantup.com/boxes/search))
```
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"
end
```
7. Launch the new virtual machine again: `vagrant up`
8. Connect to the new virtual machine: `vagrant ssh`
9. Exit from the new virtual machine: `exit`
10. Shutdown the new vm: `vagrant halt`
11. Delete the vm: `vagrant destroy`
