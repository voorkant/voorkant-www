+++
title = 'Devices'
draft = false
+++

While originally targeted at Toon 1, voorkant can run on other devices too.

## Toon 1

Specifications:

 * SoC: MCIMX27LM0P4A with:
 * CPU: ARM926EJ-S at 400 MHz
 * 128 MB memory
 * 128 MB flash, root file system 100MB, roughly 40MB free after rooting
 * Ethernet, WiFi, Z-wave, USB port
 * 800x480 display with touch, advertised as 32 bits per pixel by the framebuffer driver
 * kernel version somewhere around 2.6.36-R10-h28
 * `libc-2.21.so` with `GLIBC_` symbols `GLIBC_2.4` to `GLIBC_2.18`

Based on the libc version, it turns out that binaries copied from Debian 8/armel tend to work, if they don't need too many libraries.

To stop the stock software (this is non-permanent):

```
echo 'exit' > /tmp/etc-default-HCBv2
killall qt-gui
dd if=/dev/zero of=/dev/fb0 count=1000
```

(the `dd` is optional, but makes it clear that indeed the Toon software was stopped).

Currently (April 2024), our libcurl build needs better random than `/dev/random` on this Linux build provides, so:

```
# cd /dev ; rm random ; mknod random c 1 9
```

This is also non-permanent.

Please see [Installation](/install/) for credential setup.

You may need to use `scp -O` to get your `client-lvgl` binary onto the system.
Then, start it, and within a second or two, you should see our touch interface appear.
