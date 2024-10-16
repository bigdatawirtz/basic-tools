## SSH Remote Connection

SSH allows remote connections between hosts.

* Connect to remote server:  `ssh user@remote_server `
* Connect to remote ssh server on a different port: `ssh user@remote_server -pXXX`

## SSH authentication

SSH uses an RSA key pair to authenticate users.

* Create a RSA key pair: `ssh-keygen -t rsa`. This command creates a key pair in default diretory .ssh with default names:
  * id_rsa: private key
  * id_rsa.pub: public key
* Copy public key to server: `ssh-copy-id remote-server`. This allows automatic authentication using private key.

When you copy your public key (id_rsa.pub) to a remote server, it will be stored in ~/.ssh/authorized_keys. If you can't use commands like ssh-copy-id it is possible to copy yout key directly to that file.

## Connections config file
You can use a config file to configure your connections to remote servers. The default config file is .ssh/config
```
Host server_identificator
  HostName server_name_or_ip
  User username
  IdentityFile ~/.ssh/id_rsa #or other private key file
```

## SSH Tunneling

You can use SSH to redirect remote port from other hosts to local ports. Basic sintax:

```ssh -L local_port:ip_server_cloud:remote_port user_middle_host@middle_host_name```

For example, a tunnel from my local port 8000 to the port 80 in x.y.z.w throught host.middle.com:

```ssh -L 8000:x.y.z.w:80 host.middle.com```

## SSH Hop

Connect a remote host only reachable throug another host:

```ssh -A -t user_aux@aux_host.domain.com ssh destiny_user@destiny_host.domain.com```

Options:
- -A: enable forwarding 
- -t: force pseudo-terminal allocation