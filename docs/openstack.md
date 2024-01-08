## Openstack CLI

openstack-cli is the command line interpreter to interact with OpenStack from the console. It allows us to automate certain jobs.

### Install

openstack-cli is in the ubuntu default repositories so you can install via apt:

`sudo apt install python3-openstackclient`

Verify you have sucessfully installed openstack-cli executing the main command:

`openstack --version`

You'll se somethin like this:

```
myuser@myhost:~$ openstack --version
openstack 5.2.0
```

### Configuration

You need to download a configuration file for your account from the OpenStack web interface.

Click on the "OpenStack RC File" option from the menu of your profile in the web interface and download the configuration file.

(optional) Edit the "OpenStack RC File". Comment these lines: 

```
...
# echo "Please enter your OpenStack Password for project $OS_PROJECT_NAME as user $OS_USERNAME: "
...
# export OS_PASSWORD=$OS_PASSWORD_INPUT
...
```

Add this new line (use your own password for the cloud).

```
export OS_PASSWORD=YOUR_PASSWORD
```

#### Loading openstack-cli configuration

Every time you open a new terminal you need to execute the "OpenStack RC File" to load the configuration.

```source your_openstack_RC_file.sh```

Once the configuration is loaded you can verify the connection to the cloud by listing existing instances:

```openstack server list```

If you can see a list of the current instances on your project then the connection is ready!

You can automate the execution of the OpenStack RC File by adding the following line at the end of the bashrc file in your home directory: ~/.bashrc

```
...
source your_OpenStack_RC_File.sh
 ```

The ~/.bashrc is executed each time you open a new terminal so every new terminals will be configured to connect to your OpenStack account in the cloud.

### Using openstack-cli

#### Create an instance from command line

You can launch a new instance providing the main configuration from the CLI:

```openstack server create --image image_name --flavor flavor_name --key-name your_key_name --network network_name --security-group group_name new_instance_name```

For example:

```openstack server create --image baseos-Ubuntu-20.04-v5 --flavor m1.2c2m --key-name if_fulano --network provnet-formacion-vlan-133 --security-group aberto fulano_nova_instancia```

Verify that the new instance was launched:

```openstack server list```

Show details of your instance:

```openstack server show fulano_nova_instancia```

You can delete the new instance by doing:

```openstack server delete dani-borrame fulano_nova_instancia```

#### Create an instance with script file

You can launch a new instance providing the main configuration from the CLI and software provisioning via script file:

```openstack server create --user-data script_laboratorio_1.sh --image baseos-Ubuntu-20.04-v2 --flavor m1.2c2m --key-name if_fulano --network provnet-formacion-vlan-133 --security-group aberto fulano_nova_instancia```

