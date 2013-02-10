To download and install JUnit you currently have the following options.
 
# Plain-old JAR

Download the following JARs:

* [`junit.jar`](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22junit%22%20AND%20a%3A%22junit%22)
* [`hamcrest-core.jar`](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22org.hamcrest%22%20AND%20a%3A%22hamcrest-core%22)

To use those JARs simply put them on your test classpath.

# Maven

Add a dependency to `junit:junit` in `test` scope.  (Note: 4.11 was the latest version as of the latest edit on this page.  It may now be stale.)

    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.11</version>
      <scope>test</scope>
    </dependency>