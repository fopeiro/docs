# How to configure shared folders with Samba

This document describes a procedure to configure shared folders in Termux using Samba.

## Install Samba

Install the Samba packages from the Termux repositories:

```
pkg install samba
```

## Configuration

The default location of the Samba configuration files is ```$PREFIX/etc/samba/```, which can be created with the command:

```
mkdir $PREFIX/etc/samba/
```

Copy the sample Samba configuration file to the new folder:

```
cp $PREFIX/share/doc/samba/smb.conf.example $PREFIX/etc/samba/smb.conf
```

and change the path to the ```$HOME``` folder so that the internal storage is configured correctly:

```
sed -i s,@TERMUX_HOME@,$HOME, $PREFIX/etc/samba/smb.conf
```

## User creation

Create a new user for the Samba shares with the command:

```
smbpasswd -L -a
```

## Start the daemon

The Samba daemon can be started with the command:

```
smbd
```

## Check the configuration

If the Samba daemon has started correctly, the following command:

```
smbclient --port=4445 //192.168.x.xx/internal --user=username --password=password
```

should open an SMB session in the device.

> [!TIP]
> [A separate document](https://github.com/fopeiro/docs/blob/main/termux/Base%20configuration.md#connect-to-termux) describes the procedure to determine the IP of the device and the current username.

## Enable termux-services

The Samba service can be managed by the ```termux-services``` scripts.

To enable that, create a directory structure for smbd:

```
mkdir -p $PREFIX/var/service/smbd/log
ln -sf $PREFIX/share/termux-services/svlogger $PREFIX/var/service/smbd/log/run
```

and create a run script for the service:

```
printf '#!/data/data/com.termux/files/usr/bin/sh\nexec smbd -F -d3 2>&1' > $PREFIX/var/service/smbd/run
```

Make the run script executable with the following command:

```
chmod +x $PREFIX/var/service/smbd/run
```

Now the Samba service can be managed with the ```termux-services```, e.g. to configure Termux to run the Samba service at startup the following command would be available:

```
sv-enable smbd
```

## Map the drive from Windows

Map the Samba share from a Windows machine using the command:

```
net use Z: \\192.168.x.xx\internal /TCPPORT:4445 /user:username password
```

> [!TIP]
> In Termux, the Samba daemon is listening to port 4445 by default (instead of the usual port 445).
