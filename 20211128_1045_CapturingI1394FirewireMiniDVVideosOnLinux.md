# Capturing I1394 / Firewire MiniDV Videos On Linux



Online articles helping : 

- https://bergs.biz/blog/2017/01/26/capture-minidv-tapes-via-firewire/

- [Transferring data from a miniDV camcorder using Linux](https://blog.jonsdocs.org.uk/2020/11/25/transferring-data-from-a-minidv-camcorder-using-linux/)

- [How to Convert AVI to MP4 using FFmpeg? Lossy and Lossless Conversion](https://ottverse.com/ffmpeg-convert-avi-to-mp4-lossless/)

- http://ccrma.stanford.edu/planetccrma/man/man1/dvgrab.1.html


## Used the following so far : 

```
dvgrab --autosplit --timestamp --size 0 --rewind --format dv2 filename-
```
It would start playback on the Camcoder and grab the video in .avi file (not specifying `--format dv2` would ouput in raw .dv format)

> Compressing the video

> We can use `ffmpeg` again to compress the video without losing much quality (I didn't notice in my test run).  In my case I opted to change from AVI to MP4 using the h264 video codec and MP3 for the audio:
```
ffmpeg -i source.avi -deinterlace -vcodec h264 -acodec mp3 source.mp4
```
