This is a version of MilkyTracker modified for my own (predominantly 4-channel Protracker MOD editing) purposes, with a 
variety of UI modifications and the (hacky) inclusion of an image 
resource. 

![MilkyTracker Syphus custom](http://i.imgur.com/LEx4ZUf.png)


Mods include:

* Minimum height for custom resolutions reduced from 480 to 400
* Flat UI elements throughout, as opposed to the default (and ugly, imho) gradiented panels
* Hardcoded colour changes to sample zero-line, record dot in scopes, 'Rec' button text and slider tracks
* DELETE and BACK(space) are swapped, which is better for Mac keyboards - backspace now deletes a note, delete deletes a row
* Top/left bevels of clickable button elements are lightened slightly, for better contrast
* Lots of small changes to the pattern editor to maximise available space, reminiscent of FastTracker 2's layout: significantly, scrollbars are hidden
* Instruments and Samples listboxes are shrunk and stacked to the right 
* Added a custom button element that displays a logo image and text 
* Possibly some other stuff that I can't recall just now

Caveats: 

* This is geared towards very low resolution (ie 400px height) screen modes, and in higher modes some of the repositioning of e.g. Samples/Instruments listbox elements will look haphazard
* The Cocoa port of Milky doesn't yet allow zooming: to get a smooth upscale in fullscreen, with nice chunky pixels, use a custom resolution that's a neat divisor of your screen resolution. My laptop is 1280x800, so my Milky resolution is 640x400 and I run it fullscreen (see above). Dale will probably implement zooming for the Cocoa port further down the line using nice and smooth GPU filtering, so I'll patch that in when it happens.
* I'm mostly just making this code public for the craic, and for version control between my machines. I'd be surprised if many people's requirements of Milky are similar to mine, but if you want to mess around with it you should find it easy to build in Xcode 6 and replace the graphics with your own. It's a bit of a faff, but I'm happy to help if you get stuck.




Notes on building MilkyTracker
==============================

If you have obtained the MilkyTracker sources from the version control
repository, the autotools generated files (INSTALL, configure, etc) will
be missing. To obtain these either generate them using 'autoreconf -i'
(requires autoconf/automake to be installed) or obtain them from the
release package.

See INSTALL for a more general explanation of how 'configure' works.

The configure scripts try to check for everything needed, and will also
auto-detect ALSA and JACK adding support automatically; However, this
behaviour can be over-ridden using the following arguments to configure:

 --with-alsa | --with-jack
   Force build to use alsa/jack, build will fail if not found.
 --without-alsa | --without-jack
   Disable alsa/jack support.

Note that the configure scripts plus associated Makefiles are designed
to build the SDL version of MilkyTracker only. Build files for other
targets (OSX, win32, wince) can be found in the 'platforms' directory.


Dependencies
============

To build MilkyTracker you will need the following development libraries:

ALSA (optional)
JACK (optional)
SDL
libz

Note to package maintainers: MilkyTracker contains an internal copy of
libzzip that has been modified for use with MilkyTracker; An externally
linked libzzip will not work correctly (ZIP support will be broken).
