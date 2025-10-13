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

and open an editor to change the configuration files:

```
nano $PREFIX/etc/samba/smb.conf
```

In the configuration file, locate the \[internal\] section and change the path to the Termux shared storage:

```
[internal]
  comment = Internal storage
  path = /data/data/com.termux/files/home/storage/shared
; rest stuff unchanged
```

