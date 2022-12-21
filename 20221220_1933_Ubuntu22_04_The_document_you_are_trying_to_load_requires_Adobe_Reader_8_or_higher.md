# Ubuntu 22.04 The document you are trying to load requires Adobe Reader 8 or higher

This happens when trying to open some .pdf files downloaded from IRS websites on Ubuntu 22.04.

Some forums suggests to install an obsolete version of Adobe Reader, as Adobe does not support Linux versions anymore.

Or to install Wine, and then to install latest version of Adobe Reader for Windows and run it on Wine.

Good alternative found for me: Source https://askubuntu.com/questions/859916/is-it-possible-to-open-a-pdf-that-requires-adobe-reader-8-without-using-acroread

```
As of August 2021, Chrome 95+ also supports these files. However, to open them in Chrome, you'll need to go to chrome://flags, search for "xfa", and explicitly enable XFA support
```
It worked well for me. Just need to open .pdf via browser Chrome.
