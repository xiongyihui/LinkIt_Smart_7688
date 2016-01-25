LinkIt Smart 7688
=================


## Audio on LinkIt Smart 7688
The LinkIt Smart 7688 has an I2S interface which we can use to develop audio applications. To get audio work, extra hardware is required, for example, [the breakout board from Seeed](http://www.seeedstudio.com/depot/Breakout-for-LinkIt-Smart-7688-p-2590.html).

### Play Music
```
aplay /path/to/music.wav

madplay /path/to/music.mp3
```

### AirPlay
There are several AirPlay applications on openwrt system, such as shairport, shairport-sync and shairplay. But all these applications in LinkIt Smart 7688's repository have very poor performance. We need to patch the applications to improve their performance.

1 Shairport

  We patch shairport with [002-use_mmap.patch](shairport_patch/002-use_mmap.patch), use mmap to improve the performance and package [a new revision shairport ipk](shairport_2014-10-28-2_ramips_24kec.ipk).

  ```
  opkg update
  opkg install libdbus
  opkg install shairport_2014-10-28-2_ramips_24kec.ipk --force-checksum --force-overwrite
  shairport
  ```
  
2 Shairport-sync

  Use [shairport-sync-mini ipk](shairport-sync-mini_2.6-2_ramips_24kec.ipk)
  
  ```
  opkg install shairport-sync-mini_2.6-2_ramips_24kec.ipk --force-overwrite
  ```
  
### UPnP/DLNA
We can use [GMediaRender](https://github.com/hzeller/gmrender-resurrect) as a UPnP/DLNA server to stream audio. The GMediaRender is not in 7688's repository, we use [package feed](gmediarender) to compile an ipk file or directly use [the pre-compiled ipk](gmediarender_2013-12-04-e2eb7852eebea95c69c79c43a1e4d5f52409930f_ramips_24kec.ipk) to get GMediaRender work.

```
opkg update
opkg install libupnp gstreamer1 gst1-plugins-base gst1-mod-mad gst1-mod-audioparsers gst1-mod-id3demux gst1-mod-ogg gst1-mod-wavparse gst1-mod-flac gst1-audodetect gstreamer1-utils
```

There is a bug in mpegaudioparse of the package gst1-mod-audioparsers, which causes that the GMediaRender can't play mp3 files.

The result is that the command `gst-launch-1.0 filesrc location=/path/to/music.mp3 ! mad ! alsasink` works but the command `gst-launch-1.0 playbin uri=file:///path/to/music.mp3` doesn't.




