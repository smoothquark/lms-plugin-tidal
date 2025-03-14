# TIDAL Plugin for Squeezebox Changes

## HiRes / Dolby Atmos support
 
I have been experimenting with HiRes / Dolby Atmos support. Initial testing thus far:
 
|CLIENT ID/SECRET|LOSSLESS (16/44.1)     |HIRES LOSSLESS (24/192)|DOLBY ATMOS             |
|----------------|-----------------------|-----------------------|------------------------|
|Stock version   |Dash disabled: 16/44.1 |Dash disabled: 16/44.1 |Atmos disabled: 16/44.1 |
|                |Dash enabled: 16/44.1  |Dash enabled: 24/192   |Atmos enabled: 16/44.1  |
|TIDAL Developer |Dash disabled: 16/44.1 |Dash disabled: 16/44.1 |Atmos disabled: 16/44.1 |
|                |Dash enabled: 16/44.1  |Dash enabled: 24/192   |Atmos enabled: 16/44.1  |
|Android TV APK  |Dash disabled: fail    |Dash disabled: fail    |Atmos disabled: Atmos   |
|                |Dash enabled: 16/44.1  |Dash enabled: 24/192   |Atmos enabled: Atmos    |
 
### Notes:
1. I don't think there is any way to check what capabilities each of the client ID/secret combinations have without trial and error.
2. Regardless of the client id/secret used, sample size/rate is automatically set as 24/48,000 for HiRes and Dolby Atmos if DASH and Atmos are enabled. I think the actual stream needs to be parsed for more accurate scanning.
3. Transcoding of mpd to flac (ffmpeg) is required to playback mpd files as there is currently no native support for mpd in LMS. The manifest states mp4 with a flac codec.
4. Transcoding (ffmpeg) is required to playback Dolby Atmos by encapsulating as a 2 channel FLAC or WAV as LMS does not directly support multichannel files. I found that both FLAC and WAV work with squeezelite (squeezelite -W -c pcm,flac -o hdmi:CARD=NVidia,DEV=0) on my test system connected to a Denon AVR, but when using MPD + upmpdcli and the uPnP-Bridge, only FLAC gets passed correctly to MPD and then via HDMI to my Denon AVR.
5. I have added a custom-convert.conf with some examples that work for me. You may need to add cut and paste to your own custom-convert.conf with specific MAC addresses to get the correct set up for your system.
6. When searching for artist/albums, some Hires Lossless albums are not picked up. I think this may be because when there are identical album names and track numbers, either the Max or High versions are picked up and not both. I shall try to expolre this.
7. I am planning to add support to show [H], [M] or [A] for High, Max and Atmos albums respectively.
8. I am planning to add support to show [E] for explicit tracks.
 
## Other changes:
 
## More Thanks!
@michaelherger for his work and giving me the inspiration to go through the code to see where I can make the necessary changes.
