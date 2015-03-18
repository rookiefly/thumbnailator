# Comparisons #

The following are comparison of images created using conventional image resizing techniques, such as using the [Graphics.drawImage](http://download.oracle.com/javase/6/docs/api/java/awt/Graphics.html#drawImage(java.awt.Image,%20int,%20int,%20int,%20int,%20java.awt.image.ImageObserver)) method and [Image.getScaledInstance](http://download.oracle.com/javase/6/docs/api/java/awt/Image.html#getScaledInstance(int,%20int,%20int)) method, along with resizing using _Thumbnailator_.

## Image Quality and Rendering Speed ##

<table>
<tr align='center' valign='top'>
<td><b>Graphics.drawImage</b></td>
<td><b>Graphics.drawImage</b><br />using bilinear interpolation</td>
<td><b>Graphics.drawImage</b><br />using bicubic interpolation</td>
<td><b>Image.getScaledInstance</b><br />using <code>Image.SCALE_DEFAULT</code></td>
<td><b>Image.getScaledInstance</b><br />using <code>Image.SCALE_SMOOTH</code></td>
<td><b>Thumbnailator</b></td>
</tr>

<tr align='center'>
<td><img src='http://wiki.thumbnailator.googlecode.com/hg/img/comparison/compare-picture-drawImage.png' /></td>
<td><img src='http://wiki.thumbnailator.googlecode.com/hg/img/comparison/compare-picture-drawImageBilinear.png' /></td>
<td><img src='http://wiki.thumbnailator.googlecode.com/hg/img/comparison/compare-picture-drawImageBicubic.png' /></td>
<td><img src='http://wiki.thumbnailator.googlecode.com/hg/img/comparison/compare-picture-getScaledInstanceDefault.png' /></td>
<td><img src='http://wiki.thumbnailator.googlecode.com/hg/img/comparison/compare-picture-getScaledInstanceSmooth.png' /></td>
<td><img src='http://wiki.thumbnailator.googlecode.com/hg/img/comparison/compare-picture-thumbnailator.png' /></td>
</tr>
<tr align='center'>
<td>0 ms</td>
<td>0 ms</td>
<td>5 ms</td>
<td>422 ms</td>
<td>771 ms</td>
<td>94 ms</td>
</tr>

<tr align='center'>
<td><img src='http://wiki.thumbnailator.googlecode.com/hg/img/comparison/compare-drawImage.png' /></td>
<td><img src='http://wiki.thumbnailator.googlecode.com/hg/img/comparison/compare-drawImageBilinear.png' /></td>
<td><img src='http://wiki.thumbnailator.googlecode.com/hg/img/comparison/compare-drawImageBicubic.png' /></td>
<td><img src='http://wiki.thumbnailator.googlecode.com/hg/img/comparison/compare-getScaledInstanceDefault.png' /></td>
<td><img src='http://wiki.thumbnailator.googlecode.com/hg/img/comparison/compare-getScaledInstanceSmooth.png' /></td>
<td><img src='http://wiki.thumbnailator.googlecode.com/hg/img/comparison/compare-thumbnailator.png' /></td>
</tr>
<tr align='center'>
<td>0 ms</td>
<td>5 ms</td>
<td>5 ms</td>
<td>677 ms</td>
<td>1161 ms</td>
<td>235 ms</td>
</tr>
</table>

  * The thumbnail of the photograph in the first row was created from a 2112 pixel by 2816 pixel JPEG image.

  * The thumbnail of the image of the gradient in the second row was created from a 3000 pixel by 3000 pixel PNG image.

  * Times listed is the amount of time that each technique took to resize the image. The time is an average over three runs (using `System.currentTimeMillis`), measured on a Core 2 Duo system running Java 6 Update 21 on Windows XP.


## Code ##

The following are the relevant sections of code used to generate the above images.

### Graphics.drawImage ###
```
BufferedImage thumbnail = new BufferedImage(WIDTH, HEIGHT, BufferedImage.TYPE_INT_RGB);
		
Graphics2D g = thumbnail.createGraphics();
g.drawImage(originalImage, 0, 0, WIDTH, HEIGHT, null);
g.dispose();
```

### Graphics.drawImage using bilinear interpolation ###
```
BufferedImage thumbnail = new BufferedImage(WIDTH, HEIGHT, BufferedImage.TYPE_INT_RGB);
		
Graphics2D g = thumbnail.createGraphics();
g.setRenderingHint(RenderingHints.KEY_INTERPOLATION, RenderingHints.VALUE_INTERPOLATION_BILINEAR);
g.setRenderingHint(RenderingHints.KEY_ANTIALIASING, RenderingHints.VALUE_ANTIALIAS_ON);
g.drawImage(originalImage, 0, 0, WIDTH, HEIGHT, null);
g.dispose();
```

### Graphics.drawImage using bicubic interpolation ###
```
BufferedImage thumbnail = new BufferedImage(WIDTH, HEIGHT, BufferedImage.TYPE_INT_RGB);
		
Graphics2D g = thumbnail.createGraphics();
g.setRenderingHint(RenderingHints.KEY_INTERPOLATION, RenderingHints.VALUE_INTERPOLATION_BICUBIC);
g.setRenderingHint(RenderingHints.KEY_ANTIALIASING, RenderingHints.VALUE_ANTIALIAS_ON);
g.drawImage(originalImage, 0, 0, WIDTH, HEIGHT, null);
g.dispose();
```

### Image.getScaledInstance using `Image.SCALE_DEFAULT` ###
```
BufferedImage thumbnail = new BufferedImage(WIDTH, HEIGHT, BufferedImage.TYPE_INT_RGB);
		
Graphics2D g = thumbnail.createGraphics();
g.drawImage(originalImage.getScaledInstance(WIDTH, HEIGHT, Image.SCALE_DEFAULT), 0, 0, WIDTH, HEIGHT, null);
g.dispose();
```

### Image.getScaledInstance using `Image.SCALE_SMOOTH` ###
```
BufferedImage thumbnail = new BufferedImage(WIDTH, HEIGHT, BufferedImage.TYPE_INT_RGB);
		
Graphics2D g = thumbnail.createGraphics();
g.drawImage(originalImage.getScaledInstance(WIDTH, HEIGHT, Image.SCALE_SMOOTH), 0, 0, WIDTH, HEIGHT, null);
g.dispose();
```

### Thumbnailator ###
```
BufferedImage thumbnail = Thumbnails.of(originalImage)
        .size(WIDTH, HEIGHT)
        .asBufferedImage();
```