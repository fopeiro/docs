# How to download Spotify content from an Android phone
This document describes a procedure to download Spotify content from an Android phone.

The process involves installing a Termux environment with a Python stack that can run the Zotify script to do the actual downloads.

## Install Termux
Download Termux from a repository listed on [their webpage](https://termux.dev/en/) and install it.

> [!TIP]
> Avoid installing Termux from the Google Play Store since they are generally less tested and can have less functionality.

Update the Termux installation by running:

```
pkg update
pkg upgrade
```

### Configure Termux

Run the command:

```
termux-setup-storage
```

to give Termux permission to access the local storage.

### Install and configure OpenSSH
Install the OpenSSH package by running:

```
pkg install openssh
```

and start the SSH daemon with the command:

```
sshd
```

OpenSSH will require a login with a user and a password to open a remote SSH session, you can set the password by running:

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

Let's open a remote SSH session to Termux so I can use a real keyboard for the next steps.

### Determine the Termux username and the phone's IP address

We'll need the Termux username to open a remote SSH session, you can display it using the command:

```
whoami
```

The phone IP address can be determined by running the following commands:

```
pkg install iproute2
ip addr show
```

The output will show a bunch of information, but the relevant IP will be under wlan0 and will normally be 192.168.x.x

### Open a remote SSH session

After OpenSSH is installed, you can open a remote session to Termux from a Windows laptop using the ```ssh``` command, which is included in the default Windows installation since version 10.

```
ssh -p 8022 username@192.168.x.x
```
