# ImageComments (a Visual Studio Extension)

## Overview
This is an extension for the Visual Studio code editor that allows images to be displayed amongst code, allowing for visually rich comments. For example...

![](http://lukesdm.github.com/image-comments/media/example-1.png)

## Usage Info

### Preamble
Disclaimer: This is project is a WIP at the 
prototype stage 
and may be unstable. Please report 
issues on the GitHub repo.  

Requires: Visual Studio 2010 Standard, Premium etc. 
*(Not for 2012 yet)*; .Net 4.  
Also: currently only works in C# files

### Installation
Activate the VISX file
### How to use
Image-comments are declared with   
`/// <image url="X:\Path\To\Image.ext" *scale="Y"* />`

The `scale` attribute multiplies the source width and height by Y and is optional.

Images are displayed using the [WPF Image control](http://msdn.microsoft.com/en-us/library/ms610982) with a [BitmapFrame](http://msdn.microsoft.com/en-us/library/ms619213) source, and accepted image and URL formats are tied to those, e.g. BMP, PNG, JPG all work as image formats, and C:\Path\To\Image.png, http://www.server.com/image.png and \\server\folder\image.png all work as URLs*.


If there's a problem trying to load the image or parse the tag, the tag will be squiggly-underlined and hovering over this will show the error, e.g


![](http://lukesdm.github.com/image-comments/media/error-example-1.png)


Image-comments don't really have anything to do with XML comments, but the format is convenient and it should be pretty straight-forward to transform them for Sandcastle doc creation.


The extension adds a command in the Tools menu to toggle image-comment display on or off **.

### Uninstallation
In VS, open the Extension Manager, select ImageComments, then click uninstall. A restart of VS is required.

### Some known issues
* Absolute paths to images only.
* The caret/selection highlight height on image-comment lines grows as high the image.
* (*) Image loading from HTTP sources usually doesn't work. But if you twiddle the tag to make it invalid then valid again, it works. It's probably due to treating the asynchronous image loading process as synchronous in the implementation (which works for fast connections like hard disks).
* (**) You need to scroll/'bump' the editor window to see the effect of the on/off toggle command.

## Development Info
Requires: Visual Studio 2010 SP1 SDK

### Build instructions
Providing VS2010 SP1 SDK is installed, you should be able to build by opening the solution and hitting F6, and start debugging with the VS Experimental Instance with F5.

### Program structure
It's a very small project and may be fairly self explanatory if you are familiar with Visual Studio editor extensions.
There are two components to the extension:

* ImageCommentsEditorComponent. Contains 97% of the functionality. 
* ImageCommentsPackage. Adds a command to enable/disable functionality; VSIX definition.

For testing information, see [.\Testing\Testing.html](./testing/testing.html)
### Some known implementation issues
The code is in a semi-prototype state - it may not need a rewrite from scratch, but there's a bunch of stuff to be done

* Error/exception handling should be improved
* Program/project structure could be improved
* No automated tests and manual testing has been limited.
* There are some fairly obvious potential optimisations, but so far performance impact on plain Visual Studio seems minimal (in a release build on a 1.4GHz Core 2 Duo laptop with 1GB RAM). It would probably just add unneccessary complexity, but further testing might show otherwise.

## License
GPLv3