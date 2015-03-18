# Using Thumbnailator with Maven #

By popular demand, Thumbnailator is now available through the Maven Central Repository!

Simply add the following to the `dependencies` section of the `pom.xml`:

```
<dependency>
  <groupId>net.coobird</groupId>
  <artifactId>thumbnailator</artifactId>
  <version>[0.4, 0.5)</version>
</dependency>
```

The above dependency definition will fetch the newest available version of Thumbnailator in the 0.4.x version range.

If a specific version of Thumbnailator is required, replace `[0.4, 0.5)` with a specific version number, such as `0.4.3`.