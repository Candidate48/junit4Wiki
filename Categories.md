From a given set of test classes, the `Categories` runner
runs only the classes and methods
that are annotated with either the category given with the `@IncludeCategory`
annotation, or a subtype of that category. Either classes or interfaces can be
used as categories. Subtyping works, so if you say `@IncludeCategory(SuperClass.class)`,
a test marked `@Category({SubClass.class})` will be run.

You can also exclude categories by using the `@ExcludeCategory` annotation
 
Example:

```java
public interface FastTests { /* category marker */ }
public interface SlowTests { /* category marker */ }

public class A {
  @Test
  public void a() {
    fail();
  }

  @Category(SlowTests.class)
  @Test
  public void b() {
  }
}

@Category({SlowTests.class, FastTests.class})
public class B {
  @Test
  public void c() {

  }
}

@RunWith(Categories.class)
@IncludeCategory(SlowTests.class)
@SuiteClasses( { A.class, B.class }) // Note that Categories is a kind of Suite
public class SlowTestSuite {
  // Will run A.b and B.c, but not A.a
}

@RunWith(Categories.class)
@IncludeCategory(SlowTests.class)
@ExcludeCategory(FastTests.class)
@SuiteClasses( { A.class, B.class }) // Note that Categories is a kind of Suite
public class SlowTestSuite {
  // Will run A.b, but not A.a or B.c
}
```

## Using categories with Maven

You can use categories with either [maven-surefire-plugin][surefire] (for unit tests) or [maven-failsafe-plugin][failsafe] (for integration tests). Using either plugin, you can configure a list of categories to include or exclude. Without using either option, all tests will be executed by default.

```xml
<build>
  <plugins>
    <plugin>
      <artifactId>maven-surefire-plugin</artifactId>
      <configuration>
        <groups>com.example.FastTests,com.example.RegressionTests</groups>
      </configuration>
    </plugin>
  </plugins>
</build>
```

Similarly, to exclude a certain list of categories, you would use the `<excludedGroups/>` configuration element.

## Using categories with Gradle

Gradle's test task allows the specification of the JUnit categories you want to include and exclude.

```
test {
    useJUnit {
        includeCategories 'org.gradle.junit.CategoryA'
        excludeCategories 'org.gradle.junit.CategoryB'
    }
}
```

## Using categories with SBT

SBT's [junit-interface](https://github.com/sbt/junit-interface) allows the specification of JUnit categories via `--include-categories=<CLASSES>` and `--exclude-categories=<CLASSES>`.

[surefire]: http://maven.apache.org/surefire/maven-surefire-plugin/examples/junit.html
[failsafe]: http://maven.apache.org/surefire/maven-failsafe-plugin/examples/junit.html

## Typical usages for categories

Categories are used to add metadata on the tests. 

The frequently encountered categories usages are about:
* The type of automated tests: UnitTests, IntegrationTests, SmokeTests, RegressionTests, PerformanceTests ...
* How quick the tests execute: SlowTests, QuickTests
* In which part of the ci build the tests should be executed: NightlyBuildTests
* The state of the test: UnstableTests, InProgressTests

This is also used to add project specific metadata like which feature of a project is covered by the test.

[See usages of Junit Categories on github hosted projects ](https://github.com/search?o=asc&p=11&q=%22import+org.junit.experimental.categories.Category%22+%22%40Category%22&ref=searchresults&s=indexed&type=Code&utf8=%E2%9C%93)