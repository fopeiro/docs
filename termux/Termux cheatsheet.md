# Termux cheatsheet

This document describes several procedures that don't deserve their own page, but that I wanted to document as well.

## Access the SD card contents

The SD card contents are available in a hidden folder, its path can be determined with the command:

```
readlink -f ~/storage/external-1 | cut -d/ -f-3
```
