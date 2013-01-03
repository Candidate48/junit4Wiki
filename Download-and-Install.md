To download and install JUnit you currently have the following options.
 
# Plain-old JAR

Download one of the following JARs:

* [`junit.jar`](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22junit%22%20AND%20a%3A%22junit%22): Includes the Hamcrest classes. The simple all-in-one solution to get started quickly.
* [`junit-dep.jar`](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22junit%22%20AND%20a%3A%22junit-dep%22): Only includes the JUnit classes but not Hamcrest. Lets you use a different Hamcrest version.

To use one of those JARs simply put them on your test classpath.

# Maven

Add a dependency to `junit:junit` in `test` scope.

    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.11</version>
      <scope>test</scope>
    </dependency>