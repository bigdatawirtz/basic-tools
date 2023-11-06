## SSH authentication

SSH uses an RSA key pair to authenticate users.

* Create a RSA key pair: `ssh-keygen`. This command creates a key pair in default diretory .ssh with default names:
  * id_rsa: private key
  * id_rsa.pub: public key
* Connect to remote server:  `ssh user@remote_server `
* Connect to remote ssh server on a different port: `ssh user@remote_server -pXXX`
* Copy public key to server: `ssh-copy-id remote-server`. This allows automatic authentication using private key.

When you copy your public key (id_rsa.pub) to a remote server, it will be stored in ~/.ssh/authorized_keys. If you can't use commands like ssh-copy-id it is possible to copy yout key directly to that file.


You can use a config file to configure your connections to remote servers. The default config file is .ssh/config
```
Host server_identificator
  HostName server_name_or_ip
  User username
  IdentityFile ~/.ssh/id_rsa #or other private key file
```