## Fedora remote play setup

To solve steam black screen while using remote play on smart tv on a linux machine running Fedora (tested with version 44 with amd radeon 9000 series). 

### Launch steam with the following parameter

```
/usr/bin/steam -cef-disable-gpu
```

### Tip: You can also create a .desktop file so Krunner (on Fedora KDE) can locate and initialize it. 
Sample file

``` 
[Desktop Entry]
Version=1.0
Type=Application
Name=Steam Remote Play
Comment=Steam launched with wayland enabled remote play
Exec=/usr/bin/steam -cef-disable-gpu
Icon=steam
Terminal=true
Categories=Network;FileTransfer;Game;
MimeType=x-scheme-handler/steam;x-scheme-handler/steamlink;

```
