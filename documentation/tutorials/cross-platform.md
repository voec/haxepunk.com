---
layout: tutorial
title: Cross-Platform Deployment
permalink: documentation/tutorials/cross-platform/index.html
---

# Cross-Platform Deployment

To use HaxePunk, you'll need a library which implements the Flash API. There are currently two supported providers:

- `lime` and `openfl` (see [openfl.org](http://www.openfl.org))
- `NME` (see <https://github.com/haxenme/nme>)

With this installed, deploying for multiple plaforms is simple (if you're using NME, substitute `nme` for `lime`):

```bash
lime test flash
lime test neko

# platform specific c++ builds
lime test windows
lime test mac
lime test android
lime test ios -simulator
lime test linux
```

As long as you are on the appropriate platform OpenFL/Lime or NME will do all the work for you and compile the native version. You may need to run setup for a platform before using it. For example to build for Android you would run the following, which will prompt you to download the SDK and NDK.

```bash
lime setup android
```

Another handy trick when deploying is the _-debug_ flag. Add it to the end of any test command and you will get a version with debug symbols added. This allows you to see line numbers in a stack trace if something breaks and will enable certain debuggers to hook into your code.

## Blitting vs. Hardware Acceleration

Unlike FlashPunk it is generally not suggested to use <code>flash.display.BitmapData</code> directly due to the way rendering is handled in HaxePunk. Hardware targets use OpenGL accelerated rendering while Flash uses blitting methods <code>BitmapData.copyPixels</code>.

As long as you are utilizing the base graphic classes HaxePunk provides you should have no problem switching between targets. These are optimized for native by using objects called Atlases. If you are interested in how these work take a look at the [tutorial](/learn/tutorial/haxepunk-201-hardware-atlases) or API documentation.

## Conditional Compilation

If you need to omit a feature because it is platform specific you can use conditional compilation. This is simply done with Haxe directives.

```bash
#if flash
	// custom flash code
#elseif neko
	// custom neko code
#else
	// every other target
#end
```

The directive names should match the same target names used when building. For more information about conditional compilation check out the [OpenFL site](http://www.openfl.org/archive/developer/documentation/conditional-compilation/)
