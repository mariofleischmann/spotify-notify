# spotify-notify

spotify-notify is a cross-platform bash script to send desktop notifications with Spotify song information.
It can act as a hook for [spotifyd](https://github.com/Spotifyd/spotifyd).

https://user-images.githubusercontent.com/55689951/220197787-8d3d2a88-cf35-43f8-ac1c-cf731f4f3e8b.mp4

## Usage

```
# SYNOPSIS
#    spotify-notify [-h|--help] [-V|--version] [-v|--verbose] [--spotifyd] [ID]
#
# DESCRIPTION
#    Sends a desktop notification with Spotify song information
#
#    The song can be specified by...
#       ... passing its ID (or songlink) as an argument or
#       ... setting the TRACK_ID variable to its ID
#
# OPTIONS
#    -h, --help           Print this help
#    -V, --version        Print script version
#    -v, --verbose        Provide more detailed information
#    --spotifyd           Use script as a hook for spotifyd
#                         Notification is only sent if PLAYER_EVENT is "change"
#                         See INSTALLATION for setup instructions
```

## Installation

The [Client Credentials flow](https://developer.spotify.com/documentation/general/guides/authorization/client-credentials/)
is used to get access to the Spotify API.
Therefore, spotify-notify requires a valid Client ID and secret.
                                                                                    
### How to obtain a Client ID and Secret

* If the variables `SPOTIFY_CLIENT_ID` and `SPOTIFY_CLIENT_SECRET` are set,
they are used for authentification

* The configuration of [spotify-tui](https://github.com/Rigellute/spotify-tui) (located at `$HOME/.config/spotify-tui/client.yml`)
is automatically read if existing and variables `SPOTIFY_CLIENT_ID` and `SPOTIFY_CLIENT_SECRET` are not set
                                                                                    
### Setup spotify-notify as a spotifyd hook

spotify-notify can be registered as a [spotifyd](https://github.com/Spotifyd/spotifyd) hook in two ways:

1. Add line in configuration (`$HOME/.config.spotifyd/spotifyd.conf`):

`on_song_change_hook = "path/to/spotify-notify --spotifyd"`

2. Launch spotifyd with `--on-song-change-hook="/path/to/spotify-notify --spotifyd"`

## Supported Notifiers

`notify-send` (on Linux)

[terminal-notifer](https://github.com/julienXX/terminal-notifier) (on macOS)

## Dependencies

* `curl` (API requests)
* [jq](https://github.com/stedolan/jq) (API response parsing)
* one of the supported notifiers
* common tools like `sed`, `tail`, `tr`, `base64` for string processing
                                                              
**Optional**

* [yq](https://github.com/mikefarah/yq) (`spotify-tui` configuration parsing)
