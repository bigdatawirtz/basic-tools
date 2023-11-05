## SSH authentication

SSH uses an RSA key pair to authenticate users.

* Create a RSA key pair: `ssh-keygen`. This command creates a key pair in default diretory .ssh with default names:
  * id_rsa: private key
  * id_rsa.pub: public key
* Copy public key to server: `ssh-copy-id remote-server`. This allows automatic authentication using private key
* Connect to remote server:  `ssh user@remote_server `

You can use a config file to configure your connections to remote servers. The default config file is .ssh/config
```
Host server_identificator
  HostName server_name_or_ip
  User username
  IdentityFile ~/.ssh/id_rsa #or other private key file
```