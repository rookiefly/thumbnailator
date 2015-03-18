## Features ##

  * Create high-quality thumbnails from existing images.

> | ![http://wiki.thumbnailator.googlecode.com/hg/img/features/coobird-thumbnailator-75.png](http://wiki.thumbnailator.googlecode.com/hg/img/features/coobird-thumbnailator-75.png) | ![http://wiki.thumbnailator.googlecode.com/hg/img/features/coobird-thumbnailator-50.png](http://wiki.thumbnailator.googlecode.com/hg/img/features/coobird-thumbnailator-50.png) | ![http://wiki.thumbnailator.googlecode.com/hg/img/features/coobird-thumbnailator-32.png](http://wiki.thumbnailator.googlecode.com/hg/img/features/coobird-thumbnailator-32.png) | Thumbnailator |
|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:--------------|
> | ![http://wiki.thumbnailator.googlecode.com/hg/img/features/coobird-manual-75.png](http://wiki.thumbnailator.googlecode.com/hg/img/features/coobird-manual-75.png) | ![http://wiki.thumbnailator.googlecode.com/hg/img/features/coobird-manual-50.png](http://wiki.thumbnailator.googlecode.com/hg/img/features/coobird-manual-50.png) | ![http://wiki.thumbnailator.googlecode.com/hg/img/features/coobird-manual-32.png](http://wiki.thumbnailator.googlecode.com/hg/img/features/coobird-manual-32.png) | Graphics.drawImage |

  * Option to embed a watermark (such as a logo) in the thumbnails.
  * Transparency of the watermark is adjustable from transparent (0%) to opaque (100%).

> | ![http://wiki.thumbnailator.googlecode.com/hg/img/features/image-with-watermark-0.2f.jpg](http://wiki.thumbnailator.googlecode.com/hg/img/features/image-with-watermark-0.2f.jpg) | ![http://wiki.thumbnailator.googlecode.com/hg/img/features/image-with-watermark-0.5f.jpg](http://wiki.thumbnailator.googlecode.com/hg/img/features/image-with-watermark-0.5f.jpg) | ![http://wiki.thumbnailator.googlecode.com/hg/img/features/image-with-watermark-0.8f.jpg](http://wiki.thumbnailator.googlecode.com/hg/img/features/image-with-watermark-0.8f.jpg) | ![http://wiki.thumbnailator.googlecode.com/hg/img/features/image-with-watermark-1.0f.jpg](http://wiki.thumbnailator.googlecode.com/hg/img/features/image-with-watermark-1.0f.jpg) |
|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|

  * Supports rotation of thumbnail.

> | ![http://wiki.thumbnailator.googlecode.com/hg/img/features/image-rotated-0.png](http://wiki.thumbnailator.googlecode.com/hg/img/features/image-rotated-0.png) | ![http://wiki.thumbnailator.googlecode.com/hg/img/features/image-rotated-90.png](http://wiki.thumbnailator.googlecode.com/hg/img/features/image-rotated-90.png) | ![http://wiki.thumbnailator.googlecode.com/hg/img/features/image-rotated-180.png](http://wiki.thumbnailator.googlecode.com/hg/img/features/image-rotated-180.png) | ![http://wiki.thumbnailator.googlecode.com/hg/img/features/image-rotated-270.png](http://wiki.thumbnailator.googlecode.com/hg/img/features/image-rotated-270.png) | ![http://wiki.thumbnailator.googlecode.com/hg/img/features/image-rotated-45.png](http://wiki.thumbnailator.googlecode.com/hg/img/features/image-rotated-45.png) |
|:--------------------------------------------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------|

  * A fluent interface to simplify the process of making thumbnails programmatically.

> For example, the code in the previous example for rotating thumbnails was written as follows:
```
for (int i : new int[] {0, 90, 180, 270, 45}) {
    Thumbnails.of(new File("coobird.png"))
            .size(100, 100)
            .rotate(i)
            .toFile(new File("image-rotated-" + i + ".png"));
}
```

  * Multiple quality modes for thumbnail generation.
  * Preserves the aspect ratio of resulting thumbnail, if desired.