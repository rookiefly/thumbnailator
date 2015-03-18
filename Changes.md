## Thumbnailator 0.4.8 (December 1, 2014) ##

This release is a very minor update which includes a workaround to attempt to reduce the likeliness of `OutOfMemoryError`s from occurring. (Refer to the "`OutOfMemoryError` Workaround" section for details.)

In addition, the build tooling for Thumbnailator has been changed from Ant to Maven. ([Issue 68](https://code.google.com/p/thumbnailator/issues/detail?id=68)) This has necessitated major re-arrangement of source files to conform with the Maven project layout.

Other minor changes include updating an out-of-date comment about implementation in the `Thumbnailator` class ([Issue 68](https://code.google.com/p/thumbnailator/issues/detail?id=68)) and added line number information to the Thumbnailator JAR file to assist in debugging. ([Issue 71](https://code.google.com/p/thumbnailator/issues/detail?id=71))

Thumbnailator 0.4.8 is available via Maven, and [JAR files can be downloaded](http://search.maven.org/#artifactdetails|net.coobird|thumbnailator|0.4.8|jar) from [The Central Repository](http://search.maven.org/).

### `OutOfMemoryError` Workaround ###

Issues around `OutOfMemoryError`s have been recognized from the early stages of development of Thumbnailator. ([Issue 1](https://code.google.com/p/thumbnailator/issues/detail?id=1))

However, to fundamentally address the issue requires some dramatic design changes to the core parts of Thumbnailator which would take some time and would affect many internal parts of the library. Such changes would take time before being implemented, a temporary workaround has been added to Thumbnailator 0.4.8 to reduce the likeliness of `OutOfMemoryError`s. ([Issue 69](https://code.google.com/p/thumbnailator/issues/detail?id=69))

**The workaround is not enabled by default, as it can negatively affect the quality of the final image, and has not been extensively tested, and will not necessarily avoid `OutOfMemoryError`s.**

The workaround can be enabled by one of the following ways:

  1. Starting the JVM with an argument `-Dthumbnailator.conserveMemoryWorkaround=true`, or
  1. By setting a system property key `thumbnailator.conserveMemoryWorkaround` with the value `true`.

With the workaround enabled, a smaller version of the source image will be used to reduce memory usage, under the following conditions:

  * Both height and width have dimensions larger than 1800 pixels
  * The expected memory size of the source image will take up more than 1/4 of the available JVM free memory

**This workaround should not be considered a part of the Thumbnailator's public API.** This workaround will be removed when its no longer considered useful by the author, therefore, code invoking Thumbnailator should not depend upon this workaround being always present.


## Thumbnailator 0.4.7 (December 23, 2013) ##

This release added an user-requested feature ([Issue 51](https://code.google.com/p/thumbnailator/issues/detail?id=51)) to change the output directory of the thumbnails when using the `toFiles(Rename)` or `asFiles(Rename)` method.

The following methods have been added:
  * [`toFiles(File, Rename)`](http://thumbnailator.googlecode.com/hg-history/0.4.7/javadoc/net/coobird/thumbnailator/Thumbnails.Builder.html#toFiles(java.io.File,%20net.coobird.thumbnailator.name.Rename))
  * [`asFiles(File, Rename)`](http://thumbnailator.googlecode.com/hg-history/0.4.7/javadoc/net/coobird/thumbnailator/Thumbnails.Builder.html#asFiles(java.io.File,%20net.coobird.thumbnailator.name.Rename))

## Thumbnailator 0.4.6 (September 6, 2013) ##

### Bug fixes ###

This release addresses the following issues:

  * [Issue 54](https://code.google.com/p/thumbnailator/issues/detail?id=54) - Fixed problems where `ant` could not be used to build Thumbnailator.
    * Originally, `build.xml` depended on files created by Eclipse, but the dependency has been removed
    * Some unit test cases would only pass on Java 5, but conditional checks has been added so that it will pass on Java 5 and up. (This has been verified for Java 5, 6 and 7.)

  * [Issue 55](https://code.google.com/p/thumbnailator/issues/detail?id=55) - Fixed a bug that caused the watermark to disappear in certain circumstances when using crop.

  * [Issue 56](https://code.google.com/p/thumbnailator/issues/detail?id=56) - Fixed a bug which caused the watermark to be incorrectly positioned when the EXIF orientation metadata was used to re-orient the image.

### Changes to the `LICENSE` file ###

A change has been made to the location of the `LICENSE` file.

Originally, the `LICENSE` file was located in the `resources` directory, but it has been moved to the root.

In addition, the `LICENSE` file has been added to the `META-INF` directory of the JAR files being distributes via the downloads and via the Maven Central repository.


## Thumbnailator 0.4.5 (June 30, 2013) ##

This release addresses an issue where the Exif orientation metadata was not being used in the `Thumbnailator.createThumbnail` methods. ([Issue 43](https://code.google.com/p/thumbnailator/issues/detail?id=43))


## Thumbnailator 0.4.4 (May 23, 2013) ##

This release fixes a bug which causes `OutOfMemoryError`s when running Thumbnailator on the latest versions of Java 6 and 7 -- Java 6 Update 45 and Java 7 Update 21. ([Issue 42](https://code.google.com/p/thumbnailator/issues/detail?id=42))

Many thanks goes out to Vladimir Shomin, Will Tran <will.tran@xtremelabs.com> and others for providing valuable information in tackling this problem.


## Thumbnailator 0.4.3 (January 2, 2013) ##

### Added Exif Orientation support ###

This release adds support for using the Exif metadata to properly orient thumbnails. ([Issue 13](https://code.google.com/p/thumbnailator/issues/detail?id=13), [Issue 27](https://code.google.com/p/thumbnailator/issues/detail?id=27))

Now, the default behavior is to use the Exif metadata to determine the correct orientation of
the thumbnail.

However, this behavior can be overridden by disabling the usage of theExif metadata by calling the
[`useExifOrientation`](http://thumbnailator.googlecode.com/hg/javadoc/net/coobird/thumbnailator/Thumbnails.Builder.html?r=0.4.3#useExifOrientation%28boolean%29) method with
`false` as the argument.

### Other fixes ###

In addition, the message included in the `IOException` thrown when an error occurs while processing has been changed to better indicate what had occurred. ([Issue 27](https://code.google.com/p/thumbnailator/issues/detail?id=27))


## Thumbnailator 0.4.2 (May 6, 2012) ##

This release fixes an issue where the thumbnails are given incorrect file names when using the `Rename.SUFFIX_DOT_THUMBNAIL` or `Rename.SUFFIX_HYPHEN_THUMBNAIL` rename option,
if the original file name contains multiple "." characters.
(See [Issue 36](http://code.google.com/p/thumbnailator/issues/detail?id=36) for details.)

## Thumbnailator 0.4.1 (April 2, 2012) ##

This release changes the behavior of deciding the size of the thumbnail.

### Background ###

Up to Thumbnailator 0.4.0, the code used to determine the size of the thumbnail was rounding down (in other words, truncating) the dimensions.
For example, if the new dimension was calculated to be `15.4` or `15.6`, the resulting dimension would both be `15`.

Also, there were instances where the dimension(s) of the thumbnail could become 0, leading to an `IllegalArgumentException` being thrown
when attempting to make a thumbnail.

### Changes ###

From Thumbnailator 0.4.1, the code has been revised to round to the closest integer by using the `Math.round` method.
This means that if the new dimension was calculated to be `15.4` the resulting dimension would both be `15`, while a new dimension of `15.6` would result in the dimension being `16`.

Also, the minimum size of a thumbnail's dimension has been specified to be one. Therefore, under conditions which could lead to the thumbnail
having a dimension of zero, the dimension will be promoted to `1`, therefore, the aspect ratio of a thumbnail may not be necesarily maintained.

### Summary ###

The following summarizes the changes in thumbnail size between previous versions of Thumbnailator and the current version when using the builder interface`*` :

**From a original image with dimensions 100 x 106:**

| **version**    | **size after `.size(10, 10)`** | **size after `.scale(0.1)`** |
|:---------------|:-------------------------------|:-----------------------------|
| before 0.4.1 | 10 x 10                      | 10 x 10                    |
| 0.4.1        | 10 x 11                      | 10 x 11                    |

**From a original image with dimensions 100 x 104:**

| **version**    | **size after `.size(10, 10)`** | **size after `.scale(0.1)`** |
|:---------------|:-------------------------------|:-----------------------------|
| before 0.4.1 | 10 x 10                      | 10 x 10                    |
| 0.4.1        | 10 x 10                      | 10 x 10                    |

**From a original image with dimensions 100 x 6:**

| **version**    | **size after `.size(10, 10)`** | **size after `.scale(0.1)`** |
|:---------------|:-------------------------------|:-----------------------------|
| before 0.4.1 | `IllegalArgumentException`   | `IllegalArgumentException` |
| 0.4.1        | 10 x 1                       | 10 x 1                     |

`*` The builder interface refers to the use of the `Thumbnails` class as the entry point when making thumbnails, such as in the code below:

```
Thumbnails.of("path/to/image")
    .size(10, 10)
    .toFile("path/to/thumbnail");
```

### More information ###

The specification of the following classes have been changed in order to implement the changes of calculating the size of the thumbnails:

  * [`FixedSizeThumbnailMaker`](http://thumbnailator.googlecode.com/hg/javadoc/net/coobird/thumbnailator/makers/FixedSizeThumbnailMaker.html?r=0.4.1) class
  * [`ScaledThumbnailMaker`](http://thumbnailator.googlecode.com/hg/javadoc/net/coobird/thumbnailator/resizers/ResizerFactory.html?r=0.4.1) class


## Thumbnailator 0.4.0 (February 11, 2012) ##

This release introduces new functionality and minor changes to the API. _Please note that upgrading to the Thumbnailator 0.4.0 may require changing to existing code._

  * Introduction of the [`ResizerFactory`](http://thumbnailator.googlecode.com/hg/javadoc/net/coobird/thumbnailator/resizers/ResizerFactory.html?r=0.4.0) interface which allows finer control over the resizing of images.
    * Enables the use of alternate resizing algorithms.
    * Enables differing resizing strategies depending on the dimensions of the source and destination images.
    * Internal resizing routines have been reworked to use `ResizerFactory`'s.

  * The `ResizerFactory` class in the 0.3.x series has been essentially renamed to the `DefaultResizerFactory` class.

  * The following deprecated methods have been removed:
    * `fromFilenames(Collection<String>)`
    * `fromFiles(Collection<File>)`
    * `fromURLs(Collection<URL>)`
    * `fromInputStreams(Collection<InputStream>)`
    * `fromImages(Collection<BufferedImage>)`

Although the `from...(Collection)` method have been removed, the `from...(Iterable)` methods should be functionally equivalent for most scenarios.
For example, using a `List` as the argument of the `from...` methods will work the same as before.

The below code will work under Thumbnailator 0.3.x and 0.4.x without any modifications:

```
List<String> filenames = new ArrayList<String>();
filenames.add("path/to/image1.jpg");
filenames.add("path/to/image2.jpg");

Thumbnails.of(filenames)
    .size(200, 200)
    .toFiles(Rename.PREFIX_DOT_THUMBNAIL);
```

  * The `Rename` class now accepts an additional `ThumbnailParameter` as its argument, which enables finer control over determining a name for the resulting thumbnail image file by providing more context about the image resizing operation.

  * Added the [`crop(Position)`](http://thumbnailator.googlecode.com/hg/javadoc/net/coobird/thumbnailator/Thumbnails.Builder.html?r=0.4.0#crop%28net.coobird.thumbnailator.geometry.Position%29) method to crop the thumbnail after it has been resized while keeping the aspect ratio. This method has been added to address [Issue 24](http://code.google.com/p/thumbnailator/issues/detail?id=24).

For example, resizing the image from 240x200 to 100x100 using the `crop` method would result in the following:

![http://wiki.thumbnailator.googlecode.com/hg/img/features/crop.png](http://wiki.thumbnailator.googlecode.com/hg/img/features/crop.png)

  * Fixed two bugs in the [`Canvas`](http://thumbnailator.googlecode.com/hg/javadoc/net/coobird/thumbnailator/filters/Canvas.html?r=0.4.0) class.
    * The background color of images with transparency was being filled black when it should have been left transparent.
    * The width and height of the Canvas could potentially be altered when the `Canvas.apply` method is called multiple times.


## Thumbnailator 0.3.10 (September 4, 2011) ##

Added the [`scale(double, double)`](http://thumbnailator.googlecode.com/hg/javadoc/net/coobird/thumbnailator/Thumbnails.Builder.html?r=0.3.10#scale%28double,%20double%29)
method to create thumbnails by specifying the scaling factors for the width and height independently. This feature implements the feature request in [Issue 19](http://code.google.com/p/thumbnailator/issues/detail?id=19).

## Thumbnailator 0.3.9 (August 13, 2011) ##

  * Fixed an issue where the file extensions assigned to thumbnails would violate the principle of least surprise. (See [Issue 18](http://code.google.com/p/thumbnailator/issues/detail?id=18) for details.)

## Thumbnailator 0.3.8 (July 30, 2011) ##

  * Fixed an issue where the file that the thumbnail was written to remains open, preventing certain programs from accessing the file. (See [Issue 17](http://code.google.com/p/thumbnailator/issues/detail?id=17) for details.)

## Thumbnailator 0.3.7 (July 24, 2011) ##

Added the [`allowOverwrite(boolean)`](http://thumbnailator.googlecode.com/hg/javadoc/net/coobird/thumbnailator/Thumbnails.Builder.html?r=0.3.7#allowOverwrite%28boolean%29)
to specify the behavior of whether or not to overwrite existing files when creating thumbnails.

The `allowOverwrite(boolean)` method will affect the behavior of the following methods:

  * [`toFile(File)`](http://thumbnailator.googlecode.com/hg/javadoc/net/coobird/thumbnailator/Thumbnails.Builder.html?r=0.3.7#toFile(java.io.File))
  * [`toFile(String)`](http://thumbnailator.googlecode.com/hg/javadoc/net/coobird/thumbnailator/Thumbnails.Builder.html?r=0.3.7#toFile(java.lang.String))
  * [`toFiles(Iterable&lt;File&gt;)`](http://thumbnailator.googlecode.com/hg/javadoc/net/coobird/thumbnailator/Thumbnails.Builder.html?r=0.3.7#toFiles(java.lang.Iterable))
  * [`toFiles(Rename)`](http://thumbnailator.googlecode.com/hg/javadoc/net/coobird/thumbnailator/Thumbnails.Builder.html?r=0.3.7#toFiles(net.coobird.thumbnailator.name.Rename))
  * [`asFiles(Iterable&lt;File&gt;)`](http://thumbnailator.googlecode.com/hg/javadoc/net/coobird/thumbnailator/Thumbnails.Builder.html?r=0.3.7#asFiles(java.lang.Iterable))
  * [`asFiles(Rename)`](http://thumbnailator.googlecode.com/hg/javadoc/net/coobird/thumbnailator/Thumbnails.Builder.html?r=0.3.7#asFiles(net.coobird.thumbnailator.name.Rename))

Some changes have been made to the behavior of the methods listed above with respect to handling files which have not been written due to the destination file existing at
the time the thumbnails were being produced.

## Thumbnailator 0.3.6 (July 9, 2011) ##

  * Fixed an issue which was causing thumbnails to be incorrectly written to the destination file if it already exists. (See [Issue 14](http://code.google.com/p/thumbnailator/issues/detail?id=14) for details.)

## Thumbnailator 0.3.5 (June 18, 2011) ##

A feature has been added to create a thumbnail by only specifying either the width or height, as requested in [Issue 12](http://code.google.com/p/thumbnailator/issues/detail?id=12).

The feature will use the specified width or height (via the `width` and `height` methods) as the constraint, and create a thumbnail which preserved the aspect ratio of the original image.

For example, resizing a 400x300 image with the width constraint specified to 200, the thumbnail will be 200x150.

The code to perform the resize will be as follows:

```
Thumbnails.of("/path/to/image-400x300")
    .width(200)
    .toFile("/path/to/thumbnail-200x150")
```

![http://wiki.thumbnailator.googlecode.com/hg/img/features/width-or-height.png](http://wiki.thumbnailator.googlecode.com/hg/img/features/width-or-height.png)

The following methods were added to the `Thumbnails` fluent interface:

  * [`width(int)`](http://thumbnailator.googlecode.com/hg/javadoc/net/coobird/thumbnailator/Thumbnails.Builder.html?r=0.3.5#width%28int%29)
  * [`height(int)`](http://thumbnailator.googlecode.com/hg/javadoc/net/coobird/thumbnailator/Thumbnails.Builder.html?r=0.3.5#height%28int%29)


## Thumbnailator 0.3.4 (May 3, 2011) ##

It is now possible to specify the source region from which a thumbnail is produced, as requested in [Issue 6](http://code.google.com/p/thumbnailator/issues/detail?id=6).

For example, creating a 200x200 thumbnail from the center 400x400 region of the source image could be written like the following:

```
Thumbnails.of("/path/to/image")
    .sourceRegion(Positions.CENTER, 400, 400)
    .size(200, 200)
    .toFile("/path/to/thumbnail")
```

![http://wiki.thumbnailator.googlecode.com/hg/img/features/sourceregion.png](http://wiki.thumbnailator.googlecode.com/hg/img/features/sourceregion.png)

The following methods were added to the `Thumbnails` fluent interface:

  * [`sourceRegion(Region)`](http://thumbnailator.googlecode.com/hg/javadoc/net/coobird/thumbnailator/Thumbnails.Builder.html?r=0.3.4#sourceRegion(net.coobird.thumbnailator.geometry.Region))
  * [`sourceRegion(Position, Size)`](http://thumbnailator.googlecode.com/hg/javadoc/net/coobird/thumbnailator/Thumbnails.Builder.html?r=0.3.4#sourceRegion(net.coobird.thumbnailator.geometry.Position,%20net.coobird.thumbnailator.geometry.Size))
  * [`sourceRegion(int, int, int, int)`](http://thumbnailator.googlecode.com/hg/javadoc/net/coobird/thumbnailator/Thumbnails.Builder.html?r=0.3.4#sourceRegion(int,%20int,%20int,%20int))
  * [`sourceRegion(Position, int, int)`](http://thumbnailator.googlecode.com/hg/javadoc/net/coobird/thumbnailator/Thumbnails.Builder.html?r=0.3.4#sourceRegion(net.coobird.thumbnailator.geometry.Position,%20int,%20int))
  * [`sourceRegion(Rectangle)`](http://thumbnailator.googlecode.com/hg/javadoc/net/coobird/thumbnailator/Thumbnails.Builder.html?r=0.3.4#sourceRegion(java.awt.Rectangle))

In order to implement the source region selection feature, new interfaces and classes were added to the `net.coobird.thumbnailator.geometry` package, and
some retrofitting were done to classes such as `ThumbnailParameter` and the `ImageSource` subclasses.

The additions to _Thumbnailator_ are backward compatible, and should not affect code written against the _Thumbnailator_ 0.3.x API.


## Thumbnailator 0.3.3 (April 30, 2011) ##

  * Fixed a bug which causes an `IllegalStateException` when creating a GIF thumbnail with the compression quality settings specified. (See [Issue 9](http://code.google.com/p/thumbnailator/issues/detail?id=9) for details.)


## Thumbnailator 0.3.2 (March 21, 2011) ##

  * Added the `forceSize` method to the `Thumbnails` builder interface to force the size of the thumbnail to the specified dimensions. (equivalent to using the `size` method along with the `keepAspectRatio(false)` method.)
  * Added the `Canvas` image filter class which can be used to crop or add a border to the resulting thumbnail.


## Thumbnailator 0.3.1 (February 18, 2011) ##

  * It is now possible to use an `Iterable` to specify the original images through one of the `from` methods:
    * `fromFilenames(Iterable<String>)`
    * `fromFiles(Iterable<File>)`
    * `fromURLs(Iterable<URL>)`
    * `fromInputStreams(Iterable<? extends InputStream>)`
    * `fromImages(Iterable<BufferedImage>)`
  * Previous `from` methods which accept `Collection`s have been deprecated.


## Thumbnailator 0.3.0 (January 9, 2011) ##

This release introduces significant new functionality and changes to the API. _Please note that upgrading to the Thumbnailator 0.3.0 may require changing to existing code. (In most use cases, changes will be limited to updating `import` statements and adding exception handling. See below for details.)_

  * Enhanced support for inputs and outputs
    * Removed the restriction that the output type must be the same as the input type -- for example, Thumbnailator 0.2.x required that a thumbnail created from an image file be saved to a file.
    * It is now possible to retrieve thumbnails as an `Iterable`
      * This feature allows retrieval of thumbnails as they finish processing, rather than waiting until all thumbnails are processed.
      * This can potentially avoid `OutOfMemoryError`s, as Thumbnailator only needs to hold a reference to one thumbnail at a time.
  * Added input sources and output destinations.
    * Added support for retrieving images from `URL`s and `InputStream`s.
    * Added support for storing thumbnails to `OutputStream`s.
  * Added APIs to generate file names.
    * Newly created `net.coobird.thumbnailator.name` package contains classes to generate file names for thumbnails being saved to files.

The following are backward incompatibles changes:

  * Reorganized packages.
    * Moved `Coordinate`, `Position` and `Positions` classes to the `net.coobird.thumbnailator.geometry` package.
    * Moved the `Rename` class to the `net.coobird.thumbnailator.name` package.
    * Moved the `BufferedImages` and `ThumbnailatorUtils` classes to the `net.coobird.thumbnailator.util` package.
  * Removed deprecated methods and classes.
    * Methods and classes which were marked as deprecated in Thumbnailator 0.2.x have been removed.
  * All output methods of the fluent interface (including `asBufferedImages` and `asBufferedImage`) now throw `IOException`


## Thumbnailator 0.2.9 (December 29, 2010) ##

  * Added the `Transparency` image filter for changing the opacity of the resulting thumbnail.
  * Fixed a bug where calling the `asBufferedImage` method causes a `NullPointerException` if the original images did not originate from a `BufferedImage`.


## Thumbnailator 0.2.8 (December 22, 2010) ##

  * Minor changes were made to the `Thumbnails` builder interface.
    * Added an override for the `outputQuality` method which accepts a `double`.
    * Added null argument checks for in the configuration methods of the builder interface.
      * Checks were added to `scalingMode(ScalingMode)`, `resizer(Resizer)`, `alphaInterpolation(AlphaInterpolation)`, `dithering(Dithering)`, `antialiasing(Antialiasing)`, and `rendering(Rendering)`.
    * Added checks to see that a supported format is specified in the `outputFormat` method.
    * Added checks to the `outputFormatType` method, to ensure that the type and format parameters will not be in a state which could cause problems when saving thumbnails.


## Thumbnailator 0.2.7 (December 4, 2010) ##

  * Added methods to the `Thumbnails` builder interface to accept `Collection`s.
  * Fixed the behavior for adding a file extension to the name of the resulting thumbnail when the output format does not match the given extension.
  * Updated the `ThumbnailParamterBuilder` class to better support the current specification of the `ThumbnailParameter` class.


## Thumbnailator 0.2.6 (November 6, 2010) ##

  * Fixed an issue where saving a thumbnail with transparency to a BMP image causing an exception.
  * Changed `ThumbnailTask.write` from returning `boolean` to `void`, and added the `UnsupportedFormatException` class used to indicate that a format is not supported for the specified operation.
    * The `StreamThumbnailTask` and `FileThumbnailTask` classes have had their `write` methods modified to throw the `UnsupportedFormatException` and not return a `boolean` on return.
  * Added `Thumbnailator.createThumbnail(InputStream, OutputStream, String, int, int)` which can be used to specify the format to use for the output data.
  * Changed the `asBufferedImage` method to throw an `IllegalArgumentException` when multiple images are specified in the `Builder.of` method. This makes the behavior more consistent with the `toFile` method.
  * Removed the restriction that `Thumbnails.Builder.asBufferedImage` must have `BufferedImage`s as the source.
  * `ThumbnailMaker` classes will now throw an `IllegalStateException` when the size, aspect ratio or scaling factor is specified more than once.
    * The `FixedSizeThumbnailMaker` and `ScaledThumbnailMaker` classes have been modified due to this change.
  * Added null argument checks for the `Thumbnails.of` methods.


## Thumbnailator 0.2.5 (October 27, 2010) ##

  * Changed the `Thumbnails` class to create thumbnails with the same image type as the original image.
    * This change was made to address an issue where color distortions occurred in the resulting thumbnail when the original image was a JPEG. This occurred due to the original behavior to create a thumbnail image with an alpha channel. The default JPEG encoder implementation which ships with the JRE appears to cause color distortions for images which contain an alpha channel.
  * Changed the `FileThumbnailTask.read()` method to throw a `FileNotFoundException` when the `File` specified to obtain the original image does not exist.
  * Added and improved documentation.


## Thumbnailator 0.2.4 (October 10, 2010) ##

  * Fixed issues with the `ProgressiveBilinearResizer` class.
    * Fixed an issue which lead to quality degradations for thumbnails when the original image was less than twice the size of the thumbnail.
    * Fixed an issue with thumbnails of transparent images containing magnified images of the thumbnail in the background.


## Thumbnailator 0.2.3 (October 9, 2010) ##

  * The `Thumbnails` class is now the entry-point into the fluent interface of _Thumbnailator_.
    * The non-fluent interface methods have been moved from the `Thumbnails` class to the `Thumbnailator` class.
    * The non-fluent methods such as `createThumbnails` remain in the `Thumbnails` class, however, they have been deprecated and will be removed in the next major revision of _Thumbnailator_.
  * The `Thumbnails.Rename` has been promoted to a top-level class.
    * The class remains available in the `Thumbnails` class, however, it has been deprecated and will be removed in the next major revision of _Thumbnailator_.
  * Added the `Thumbnails.resizer` to specify the `Resizer` to use when creating thumbnails.


## Thumbnailator 0.2.2 (October 3, 2010) ##

  * Added new builder interface to `Thumbnails` class.
  * Many changes to support the new builder interface.
  * Added documentation and fixed bugs.


## Thumbnailator 0.2.1 (September 23, 2010) ##

  * Changed the resizing routine to improve image quality.
  * Fixed issue with trying to set compression parameters for codecs which don't support compression.
  * Added checks for allowed values for method arguments in many locations.
  * Changed the signature of `Thumbnails.createThumbnailCollection` method.
  * Fixed issue with color distortion in JPEG images by adding a workaround when writing to JPEGs.


## Thumbnailator 0.2.0 (September 21, 2010) ##

  * Initial release.