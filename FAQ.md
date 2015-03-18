# Frequently Asked Questions #

## Which image formats are supported by Thumbnailator? ##

The image reading and writing functionality of Thumbnailator is dependent on the capability of the [Java Image I/O API](http://docs.oracle.com/javase/7/docs/technotes/guides/imageio/) which the library uses.

By default, Java 6 and beyond support reading and writing of JPEG, PNG, GIF, BMP and WBMP formats; Java 5 did not support writing GIF files.

Sources:
  * Java 5: http://docs.oracle.com/javase/1.5.0/docs/api/javax/imageio/package-summary.html#package_description
  * Java 6: http://docs.oracle.com/javase/6/docs/api/javax/imageio/package-summary.html#package_description
  * Java 7: http://docs.oracle.com/javase/7/docs/api/javax/imageio/package-summary.html#package_description

The Image I/O API has a plug-in mechanism to support additional image formats.

As Thumbnailator uses the Image I/O API, by using additional Image I/O plug-ins, it is possible to support more formats from within Thumbnailator.