To download and install JUnit you currently have the following options.
 
# Plain-old JAR

Download the following JARs and put them on your test classpath:

* [`junit.jar`](http://bit.ly/My9IXz)
* [`hamcrest-core.jar`](http://bit.ly/1gbl25b)

# Maven

Add a dependency to `junit:junit` in `test` scope.  (Note: 4.12 is the latest stable version as of the latest edit on this page.)

    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.12</version>
      <scope>test</scope>
    </dependency>