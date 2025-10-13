# How to download Spotify content

This document describes a procedure to download Spotify content from an Android phone.

The process involves installing a Termux environment with a Python stack that can run the Zotify script to do the actual downloads.

## Install Termux

[A separate document](https://github.com/fopeiro/docs/blob/main/termux/Base%20configuration.md) describes the procedure to do a base installation of Termux.

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

> [!TIP]
> The Zotify script was originally released in the [project's git repository](https://github.com/zotify-dev/zotify), but the installation procedure is not working anymore and the project is no longer maintained, so this document is using the [Googolplexed0 fork](https://github.com/Googolplexed0) instead.

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
  --root-path $HOME/storage/downloads/zotify     `#Save downloaded tracks in the internal storage` \
  --output "{song_name} - {artist}"              `#Downloaded file names` \
  --download-format mp3                          `#Downloads in MP3 format` \
  --download-lyrics False                        `#Avoid downloading lyrics on separate files`
```
