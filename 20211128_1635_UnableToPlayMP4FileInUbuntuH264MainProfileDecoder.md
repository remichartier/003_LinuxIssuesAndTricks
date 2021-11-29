# Unable to play MP4 file in Ubuntu 18.04: H.264 (Main Profile) decoder is required to play the file, but is not installed

This trick is from this webpage https://ourcodeworld.com/articles/read/980/unable-to-play-mp4-file-in-ubuntu-18-04-h-264-main-profile-decoder-is-required-to-play-the-file-but-is-not-installed

> Learn how to solve the issue of playing an MP4 video on Ubuntu 18.04.

> Unable to play MP4 file in Ubuntu 18.04: H.264 (Main Profile) decoder is required to play the file, but is not installed

> New users in Ubuntu will notice that for some reason, a lot of audio and video codecs aren't available immediately in Ubuntu, unlike Windows or Mac. This happens basically for legal and technical reasons. Ubuntu excludes these codecs because these video files and other media formats are copy-right protected, so you can't just add these protected technology to your operating systems and programs without agreeing to their licensing terms and conditions. The error is basically is the following one:

> H.264 (Main Profile) decoder are required to play the file, but are not installed.

> The solution for this issue is basically to install the missing codecs with the terminal in your system. For this, search for the terminal of Ubuntu and type the following commands. The first command will update the repositories:

> `sudo apt-get update`

> Then install the following packages that contain the most common codecs for video players:

> `sudo apt-get install libdvdnav4 libdvdread4 gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly libdvd-pkg`

> These packages are:

> - libdvd: libdvdnav is a DVD navigation library, which provides an interface to the advanced features of DVDs, like menus and navigation. It contains the VM and other parts useful for writing DVD players. It's based on Ogle, but was modified to be used by xine and mplayer.
> - gstreamer: GStreamer is a plugin to install codecs using QApt.

> After installing the previous packages, proceed with the installation of the Ubuntu restricted extras with the following command:

> `sudo apt-get install ubuntu-restricted-extras`

> The ubuntu-restricted-extras package allows users to install ability to play popular non-free media formats, including DVD, MP3, Quicktime, and Windows Media formats. After running the commands, Ubuntu should be able immediately to play those videos that failed to play previously. If it doesn't, try restarting the computer and try to play the video again and it should work.

Note : 
- On Ubuntu 20.04 : 
```
Package libdvdread4 is not available, but is referred to by another package.
This may mean that the package is missing, has been obsoleted, or
is only available from another source

E: Package 'libdvdread4' has no installation candidate
```
-----> Need to install libdvdread7 instead of libdvdread4
