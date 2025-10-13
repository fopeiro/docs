# Base configuration

This document describes a procedure to install Termux in an Android phone, configure SSH to enable remote logging and open a remote session in the terminal.

## Install Termux

Download Termux from a repository listed on [their webpage](https://termux.dev/en/) and install it.

> [!TIP]
> Avoid installing Termux from the Google Play Store since they are generally less tested and can have less functionality.

### Post-installation

Update the Termux installation by running:

```
pkg update
pkg upgrade
```

and give Termux permission to access the phone's local storage with the command:

```
termux-setup-storage
```

### Install OpenSSH

Install the OpenSSH package by running:

```
pkg install openssh
```

and start the SSH daemon with the command:

```
sshd
```

OpenSSH will require a login with a user and a password to open a remote SSH session, you can set the password for the current user by running:

```
passwd
```

> [!TIP]
> To configure Termux to run OpenSSH when starting the application, run the following commands:
> 
> ```
> pkg install termux-services
> sv-enable sshd
> ```

## Connect to Termux

After OpenSSH is installed, you can open a remote session to Termux from a Windows laptop using the ```ssh``` command, which is included in the default Windows installation since version 10.

### Determine the Termux username

We need to know the Termux username to open a remote SSH session, you can display it using the command:

```
whoami
```

### Determine the phone IP address

The phone IP address can be determined by running the following commands:

```
pkg install iproute2
ip addr show
```

The output will show a bunch of information, but the relevant IP will be under wlan0 and will normally be 192.168.x.x

### Open a remote SSH session

Open an SSH connection to Termux using the command:

```
ssh -p 8022 username@192.168.x.x
```

> [!TIP]
> In Termux, the SSH daemon is listening to port 8022 by default (instead of the usual port 22).

## Display system information

Install the neofetch package by running:

```
pkg install neofetch
```

and display information about the Termux system with the command:

```
neofetch
```
