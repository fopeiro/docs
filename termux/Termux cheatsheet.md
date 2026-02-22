# Termux cheatsheet

This document describes several procedures that don't deserve their own page, but that I wanted to document as well.

## Basic packages

Install several basic packages with the command:

```
pkg install neofetch micro openssh rclone termux-services wget
```

## Micro configuration

Set the Micro editor configuration with the following command:

```
printf '{\n    "clipboard": "terminal"\n}\n' > $HOME/.config/micro/settings.json
```
