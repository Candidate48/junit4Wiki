To download and install JUnit you currently have the following options.
 
# Plain-old JAR

Download the following JARs and add them to your test classpath:

* [`junit.jar`](https://search.maven.org/search?q=g:junit%20AND%20a:junit)
* [`hamcrest-core.jar`](https://search.maven.org/search?q=g:org.hamcrest%20AND%20a:hamcrest-core)

# Maven

Add a dependency to `junit:junit` in `test` scope.  (Note: 4.12 is the latest stable version as of the latest edit on this page.)

    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.12</version>
      <scope>test</scope>
    </dependency>

# Gradle

See [[Use-with-Gradle]]