# Gradle Dependency

Make sure these lines are in your build.gradle

```groovy
apply plugin: 'java'

dependencies {
  testCompile 'junit:junit:4.12'
}
```

# Execution

See [Gradle Java tests](http://www.gradle.org/docs/current/userguide/java_plugin.html#sec:java_test) for configuration information. In short:

    ./gradle test

# Using Hamcrest

## JUnit 4.11 and later

There is nothing extra that needs to be done in order to use a specific artifact of Hamcrest. In the past, there were two JUnit Maven artifacts: `junit:junit` and `junit:junit-dep`, where the latter version did not include a bundled copy of `org.hamcrest:hamcrest-core` and instead declared a transitive dependency on Hamcrest. In order to be more Maven-like, starting in version 4.11, there is only the `junit:junit` artifact which uses a transitive dependency on `hamcrest-core`.

## JUnit 4.10 and earlier

Instead of using `junit:junit` as your test dependency, you should use `junit:junit-dep` along with specifying a particular Hamcrest library dependency beforehand. For example:

```groovy
dependencies {
  testCompile group: 'org.hamcrest', name: 'hamcrest-core', version: '1.3'
  testCompile group: 'junit', name: 'junit-dep', version: '4.10'
  testCompile group: 'org.hamcrest', name: 'hamcrest-library', version: '1.3'
  testCompile group: 'org.mockito', name: 'mockito-core', version: '1.9.+'
}
```