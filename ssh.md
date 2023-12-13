## SSH

Topics

### What is ssh
The secure shell protocol (ssh) is is a cryptographic network protocol for operating secure communications over and unsercured network. ssh application (like openssh, etc) are based on a client-server architecture. The ssh server listens to the network for SSH requests and provides a cli for the system running the server. the ssh client is the aplication that conects to remote servers.

#### SSH Authentication using password
SSH can authenticate users by two ways: passwords or SSH Keys. This is a less secure method but it is necessary in order to set up the remote computer for SSH key pair. For this method you need to know thre things: 1. the ip address of the remote computer, 2. the user name, and its password. In the example below I'm connecting to user pi in a local network.

```
ak@AKM2 ~ % ssh pi@192.168.0.123                                                       
pi@192.168.0.123's password: 
Linux raspberrypi 6.1.21-v8+ #1642 SMP PREEMPT Mon Apr  3 17:24:16 BST 2023 aarch64

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
Last login: Wed Dec 13 15:23:42 2023 from 192.168.0.47

SSH is enabled and the default password for the 'pi' user has not been changed.
This is a security risk - please login as the 'pi' user and type 'passwd' to set a new password.

pi@raspberrypi:~ $ 
```

#### SSH Authentication using key pairs
The latter authentication method is deemed more secure. SSH keys are are key-pair comprise of a public and private keys. Publics keys can be shared without concern, while private keys need protected. 

### Generating ssh key pair and distributing public keys
* Connecting to remote machienes using ssh
* Setting up ssh without password
* Setting up ssh connection with github
* Setting up ssh connection with rapsberry pi
* Setting up VSCode for woring on remote machienes
* 

```
This is some code
```


