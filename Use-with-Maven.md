# Maven Dependency

```xml
<dependency>
  <groupId>junit</groupId>
  <artifactId>junit</artifactId>
  <version>4.11</version>
  <scope>test</scope>
</dependency> 
```

## Execution

See [Maven Surefire plugin](http://maven.apache.org/plugins/maven-surefire-plugin/), and, for Integration Testing the [Maven Failsafe Plugin](http://maven.apache.org/surefire/maven-failsafe-plugin/)

## Use JUnit and Hamcrest in Maven

### Version 4.11 and later

Up until now there were two Maven artifacts for JUnit: `junit:junit-dep` and `junit:junit`. From a Maven point-of-view only the former made sense because it did not contain the Hamcrest classes but declared a dependency to the Hamcrest Maven artifact. The latter included the Hamcrest classes which was very un-Maven-like.

From this release (4.11) on, you should use `junit:junit` which will be what `junit:junit-dep` used to. If you still reference `junit:junit-dep`, Maven will automatically relocate you to the new `junit:junit` and issue a warning for you to fix.

### Version 4.10 and earlier

In your `pom.xml`, declare dependency used as `junit-dep`, and also override transitive dependency to `hamcrest-core`, so you can use Hamcrest full library of matchers:

```xml
<dependency>
  <groupId>org.hamcrest</groupId>
  <artifactId>hamcrest-core</artifactId>
  <version>1.3</version>
  <scope>test</scope>
</dependency>
<dependency>
  <groupId>junit</groupId>
  <artifactId>junit-dep</artifactId>
  <version>4.10</version>
  <scope>test</scope>
</dependency>         
<dependency>
  <groupId>org.hamcrest</groupId>
  <artifactId>hamcrest-library</artifactId>
  <version>1.3</version>
  <scope>test</scope>
</dependency>
<dependency>
  <groupId>org.mockito</groupId>
  <artifactId>mockito-core</artifactId>
  <version>1.9.0</version>
  <scope>test</scope>
</dependency>
```

## Discover slowest test from Surefire xml output:

The following one-liner described [here](http://stackoverflow.com/questions/5094410/how-to-list-the-slowest-junit-tests-in-a-multi-module-maven-build).

Reports on the test times, slowest sorted to the top:

```bash
$ grep -h "<testcase" `find . -iname "TEST-*.xml"` | sed 's/<testcase time="\(.*\)" classname="\(.*\)" name="\(.*\)".*/\1\t\2.\3/' | sort -rn | head
```