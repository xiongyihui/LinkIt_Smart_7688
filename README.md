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
  opkg install libdbus
  opkg install shairport_2014-10-28-2_ramips_24kec.ipk --force-checksum --force-overwrite
  shairport
  ```

