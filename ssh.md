# SSH

## What is ssh
The secure shell protocol (SSH) is is a cryptographic network protocol for operating secure communications over and unsercured network. SSH application (like openssh, etc) are based on a client-server architecture. The SSH server listens to the network for SSH requests and provides a CLI for the system running the server. The SSH client is the aplication that conects to remote servers securelly, which means authentication is a cornerstone of using SSH. This is how to authenticate through SSH:

## SSH Authentication using password
SSH can authenticate users by two ways: passwords or SSH Keys. This is a less secure method but it is necessary in order to set up the remote computer for SSH key pair. For this method you need to know: 1. the ip address of the remote computer, 2. the user name, and 3. its password. In the example below I'm connecting to user pi in a raspberry pi connected to local network.

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

pi@raspberrypi:~ $ 
```

You're done! Now you can interact throgh the CLI.

When you're ready to terminate the connection just type the *Ctrl-d* key binding or just type following command:

```
29 pi@raspberrypi:~ $ exit
```


---


## SSH Authentication using key pairs
SSH authentication using key pair preferred method over password login as its more secure. SSH keys are a pair of public and private keys that enable authentication with the remote machine. Public keys can be shared without concern, while private keys need protected.


### Generating ssh key pair and distributing public keys
Key pairs are generated using the ssh-keygen command as follows:

```
$ ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/user/.ssh/id_rsa):

```
Enter and renter the passphrase when promted (if applicable). You can add or remove the passphrase after generating the key pair, see below. The whole interaction should look like this:

```
$ ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/user/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /Users/user/.ssh/id_rsa
Your public key has been saved in /Users/user/.ssh/id_rsa.pub
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
$ 
```
### Generating multiple key pairs for auth at multiple remote servers
In case you'd like to create multiple keys use following command so that you can create multiple keys with different associations and anmes.
```
ssh-keygen -t rsa -C "name@personal_email.com"
```
Give it a suitable name that describes the keys purpose like `id_rsa_personal`. This naming will be important later on when you set ssh config so that it know which key pair to choose depending on the host server name. More on that later. 



### Distributing public keys

In order to distribute public keys from the local machine to remote (host) server, requires adding the the public key in /Users/user/.ssh/id_rsa.pub from the local machine to the host machine under ~/.ssh/athorized keys. Alternatively, you can execute the command below from your local machine in order to add the public key to the remote server.

```
 $ ssh-copy-id -i ~/.ssh/id_rsa.pub pi@192.168.0.123
```
Where _pi_ is user, _ ~/.ssh/id_rsa.pub_ is the location of the public key on the local machine and hthe IP address corresponds to the remote server. 


### Managing key pair passphrases

Sometimes you want to add or remove a passphrases associated to the key pair you just generated. For example, accessing a remote host via VSCode without passphrase makes things easier. 

To add change or remove a passhphrase to an existing key pair exeucute the following command:

```
$ ssh-keygen -p -f ~/ssh/id_rsa
> Enter old passphrase: [Type old passphrase]
> Key has comment 'your_email@example.com'
> Enter new passphrase (empty for no passphrase): [Type new passphrase]
> Enter same passphrase again: [Repeat the new passphrase]
> Your identification has been saved with the new passphrase.
```

You'll be prompted to enter the passphrase if applicable. To remove the passphrase just leave the passphrase blank and hit enter. 

## Organizing your ssh config file for a single ssh key pair
You can apply changes to .ssh config file in order preset some parameters and create an alias so that you don't have recall repetitive information when ssh-ing into a remote machine. This [article](https://linuxize.com/post/using-the-ssh-config-file/) and this [video](https://www.youtube.com/watch?v=MWqfc_fegVg) are a good summary on how to create and apply changes to your config file. Configuring the ssh config file is not only useful when managing a single key, but, more so when managing multipl

The syntax is very simple and you can set some important parameters: 

```
HOST alias of the remote machiene
    HostName {host ip adress} or {host fully qualified domain name}
    User `{host user name}`
    Port {port number}
 ```
For example, if you want to ssh into a remote server hosted ad ip address `192.168.123.123`, and the login name is `pi` and the name of the host is `raspberry` you'd have folling 

```
HOST raspbery
    HostName 192.168.123.123
    User pi
    Port 2222
```
No you can ssh into remote machiene locate at the above ip address, as user pi, using port 2222 with just following command: 

```
ssh raspberry
```


## Managing multiple ssh key pairs
You may want to create multiple ssh key pair for multiple reasons. You'll may need to connect to multiple remote hosts, and for security reasons, and you want to connect to each machiene with only one key pair. Another scenario is that you may have to connect to remote host that may be work related and business related. In these cases you can issue two key pair for each remote server. This [article](https://connkat.medium.com/setting-up-multiple-ssh-keys-on-one-computer-75f068d972d9) is a quick guide on how to set up multiple key pairs.

Create an ssh key for your private needs
```
ssh-keygen -t rsa -C "name@personal_email.com"
```
When prompted make sure the change the default name to something meaning like `id_rsa_personal`.
Now do the same for the other ssh key pair and give an expressive name like `id_rsa_company`.

Now, so that your client know which key pair to use, make sure to update ssh `config` file or create it if it doesn't exist. 
```
# Work account
Host bitbucket.org
HostName bitbucket.org
IdentityFile ~/.ssh/id_rsa_work
User git
IdentitiesOnly yes

# Personal account
Host github.com
HostName github.com
IdentityFile ~/.ssh/id_rsa_personal
User git
IdentitiesOnly yes
```

Now you should be done, and can move on to storing the public keys on the respective remote servers. There may some issues depending on host configuration and requirments that can be addressed as needed. 

## Setting up VSCode for working on remote machines

In order to setup development on remote host on VS code follow these steps: 

1. On VSCode install following extension: [Remote - SSH](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-ssh)
2. Make sure you set up SSH between machines (see above)
3. Select *Remote-SSH: Connect to Host...* from the command palette
4. Enter the remote host name, e.g. pi@raspberry, and hit enter. 
5. You're done!
