## SSH

Topics

### What is ssh
The secure shell protocol (ssh) is is a cryptographic network protocol for operating secure communications over and unsercured network. ssh application (like openssh, etc) are based on a client-server architecture. The ssh server listens to the network for SSH requests and provides a cli for the system running the server. the ssh client is the aplication that conects to remote servers.

#### SSH Authentication using password
SSH can authenticate users by two ways: passwords or SSH Keys. This is a less secure method but it is necessary in order to set up the remote computer for SSH key pair. For this method you need to know: 1. the ip address of the remote computer, 2. the user name, and its password. In the example below I'm connecting to user pi in a raspberry pi connected to local network.

```
$ ~ % ssh pi@192.168.0.123                                                       
pi@192.168.0.123's password:
```
```
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
You're done, now you can interact throgh the command line.

When you're ready to terminate the connection just type the *Ctrl-d* key binding or just type following command:
```
29 pi@raspberrypi:~ $ exit
```


### SSH Authentication using key pairs
SSH authentication using key pair is more secured and the preferred method over password login. SSH keys are are key pair are comprises of a public and private keys. Publics keys can be shared without concern, while private keys need protected.



### Generating ssh key pair and distributing public keys
Key pairs are generated using the ssh-keygen command as follows:

```
$ ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/ninovillaflor/.ssh/id_rsa):
```
Enter and renter the passphrase when promted (if applicable). The whole interaction should look like this:

```
ak@AKM2 .ssh % ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/##/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /Users/##/.ssh/id_rsa
Your public key has been saved in /Users/##/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:X/uA+zFeSSyVv1nLV5HTmCUVN/RSxsQRWzf5eHIYY40 ##@####.#####
The key's randomart image is:
+---[RSA 3072]----+
|              o##|
|              EX#|
|             .*X+|
|             o+o*|
|        S   o o++|
|         . o +..*|
|          o = o=.|
|           o *  .|
|          ..o .  |
+----[SHA256]-----+
ak@AKM2 .ssh % 
```

### Distributing public keys
In order to distribute public keys from the local machine to remote (host) server, requires adding the the public key in /Users/user/.ssh/id_rsa.pub from the local machine to the host machine under ~/.ssh/athorized keys. Alternatively, you can execute the command below from your local machine in order to add the public key to the remote server.

```
 pi@raspberrypi:~ $ ssh-copy-id -i ~/.ssh/id_rsa.pub pi@192.168.0.123
```
Where _pi_ is user, _ ~/.ssh/id_rsa.pub_ is the location of the public key on the local machine and hthe IP address corresponds to the remote server. 

## Setting up VSCode for woring on remote machienes
 

