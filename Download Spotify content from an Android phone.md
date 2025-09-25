# How to download Spotify content from an Android phone

This document describes a procedure to download Spotify content from an Android phone.

The process involves installing a Termux environment with a Python stack that can run the Zotify script to do the actual downloads.

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

## Install Zotify

Follow the [installation instructions from the Zotify documentation](https://github.com/Googolplexed0/zotify).

We'll first install the libraries used by Zotify:

```
pkg install python3 git ffmpeg
```

and then we need to get the pipx tool:

```
python3 -m pip install --user pipx
$HOME/.local/bin/pipx ensurepath
```
Now we can install the Zotify script:

```
pipx install git+https://github.com/Googolplexed0/zotify.git
```

## Provide Spotify credentials

**In a Termux session running in the phone**, run the Zotify script:

```
zotify
```

It will output a URL to link Spotify with the link to authorize an application.

Copy the URL and paste it in the phone's web browser, and then click the button to authorize the application.

The ```zotify``` instance running in the Termux session should detect the authorization and handle the provided credentials.

## Download Spotify content

A sample command to download Spotify content using a Zotify command with the options that I normally use would be:

```
zotify <track/album/playlist/episode/artist url> `#Track, album, playlist to download` \
  --root-path ~storage/downloads/zotify          `#Save downloaded tracks in the internal storage` \
  --output "{song_name} - {artist}"              `#Downloaded file names` \
  --skip-existing                                `#Skip songs with the same file name` \
  --download-format mp3                          `#Downloads in MP3 format` \
  --download-lyrics False                        `#Avoid downloading lyrics on separate files`
```
