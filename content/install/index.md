+++
title = 'Installation'
draft = false
+++

TODO: avoid `$ ` in copy (for pasting) of commands. https://css-tricks.com/to-or-not-to-displaying-terminal-code-snippets/ is interesting, but not sure how to fold it into markdown. https://discourse.gohugo.io/t/set-custom-classes-within-markdown-content/20627/3 from 2019 notes that hugo's MD renderer, Goldmark, can only do custom classes on headings, and this appears to still be true.

## Usage on your local system

### Compile from source

This section is for local running.
Scroll down [FIXME anchor link] for deployment to other devices.

You will need a very recent Meson version.
1.0.1 is too old, 1.3.2 works. [FIXME figure out exact version and also put it in `meson.build` as `meson_version` req].
`pipenv` or other Python virtual env managers should make it easy to get one.

[git clone, mention submodules]

To build for Debian 12, something like this works:

```
$ sudo apt install build-essential cmake meson ninja-build nlohmann-json3-dev pkg-config libssl-dev libsdl2-dev
$ meson setup build/
$ meson compile -C build/
```

FIXME explain our `-D` things, like we use in the armel build below.

voorkant should also build on macOS - see the `build-macos` job in [our GitHub Actions build workflow](https://github.com/voorkant/voorkant-core/blob/main/.github/workflows/main.yml) for hints.
Turning this into actual documentation would be a welcome PR!

### Get access to your Home Assistant installation

In the Home Assistant web interface, click your user name (bottom left), this takes you to `/profile`.
Scroll down and create a Long-Lived Access Token.

Don't forget to save it.
A convenient method is to make a file `.secrets` inside your `voorkant-core` checkout with content like this:

```
HA_WS_URL=ws://localhost:8123/api/websocket
HA_API_TOKEN=[secret goes here]

export HA_WS_URL
export HA_API_TOKEN
```

Note that [`wss://` (websockets with SSL/TLS) is currently not supported](https://github.com/voorkant/voorkant-core/issues/57).

### Running

To run the FTXUI terminal frontend:

```
$ . .secrets
$ build/voorkant-ftxui
```

To run the LVGL frontend (compiled against SDL by default, which will handle creating a window for it and taking mouse/touch input):

```
$ . .secrets
$ build/voorkant-lvgl entity light.*
```

(the run syntax of voorkant-lvgl is subject to occasional changes, run `build/voorkant-lvgl help` to find today's syntax.)

Finally, `build/voorkant-cli` has a collection of useful small tools.

## Compiling for another target

The only target currently supported and tested is [Eneco Toon 1](/devices/#toon-1).

You will need Docker+QEMU with a working binfmt setup [link?].

First, build a Debian armel image to do our compilation in:

```
$ cd scripts/build-targets && make armel
$ cd ../..
```

Then set up Meson, and do the build:

```
$ scripts/build-targets/run armel sh -c 'LDFLAGS="-static -latomic" meson setup build-armel --prefer-static -Dbuildtype=release -Dlvgl-driver=fbdev -Dfront-ftxui=disabled'
$ scripts/build-targets/run armel sh -c 'meson compile -C build-armel'
```

After a very long time, you will find binaries in `build-armel/`.

## Downloading pre-built binaries

[something something github actions]
