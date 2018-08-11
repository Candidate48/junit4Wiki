To download and install JUnit you currently have the following options.
 
# Plain-old JAR

Download the following JARs and add them to your test classpath:

* [`junit.jar`]http://www.java2s.com/Code/Jar/j/Downloadjunit410jar.htm
* [`hamcrest-core.jar`]

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