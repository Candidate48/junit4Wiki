欢迎来到 JUnit wiki!
* [[下载和安装]]
* [[开始]]
* 版本记录
  * [[4.13|4.13-release-notes]] - (unreleased)
  * [4.12](https://github.com/junit-team/junit/blob/master/doc/ReleaseNotes4.12.md) - (released December 4, 2014)
  * [4.11](https://github.com/junit-team/junit/blob/master/doc/ReleaseNotes4.11.md)
  * [4.10](https://github.com/junit-team/junit/blob/master/doc/ReleaseNotes4.10.md)
  * [4.9.1](https://github.com/junit-team/junit/blob/master/doc/ReleaseNotes4.9.1.md)
  * [4.9](https://github.com/junit-team/junit/blob/master/doc/ReleaseNotes4.9.md)
* [[Maintainer Documentation]]
* [[Deprecation Policy]]
* [[I want to help!]]
* [Latest JUnit Questions on StackOverflow](https://stackoverflow.com/questions/tagged/junit)
* [Latest JUnit API JavaDocs](http://junit.org/javadoc/latest/)

##  JUnit Usage and Idioms
* [[Assertions CN]] - 单元测试的必要语句
* [[Test Runners]] - how tests should be executed
* [[Aggregating tests in Suites]] - how to combine multiple related tests into a test suite
* [[Test Execution Order]] - specifying what order to run unit tests
* [[Exception Testing]] - how to specify expected exceptions in unit tests
* [[Matchers and assertThat]] - how to use Hamcrest matchers and more descriptive assertions
* [[Ignoring Tests]] - how to disable test methods or classes
* [[Timeout for Tests]] - how to specify maximum execution times for tests
* [[Parameterized Tests]] - writing tests that can be executed multiple times with different parameter values
* [[Assumptions with Assume]] - similar to assertions, but without making tests fail
* [[Rules]] - stop extending abstract test classes and start writing test rules
* [[Theories]] - write tests that are more like scientific experiments using randomly generated data
* [[Test Fixtures]] - specify set up and clean up methods on a per-method and per-class basis
* [[Categories]] - group your tests together for easier test filtering
* [[Use with Maven]] - how to use JUnit with your Maven build
* [[Use with Gradle]] - how to use JUnit with your Gradle build
* [[Multithreaded code and Concurrency]] - basic ideas behind testing concurrent code
* [[Java contract test helpers]]
* [[Continuous Testing]]

##  Third-party extensions

* [[Custom Runners]]
* [net.trajano.commons:commons-testing for UtilityClassTestUtil](http://site.trajano.net/commons-testing/) per #646
* [System Rules](http://stefanbirkner.github.io/system-rules) – A collection of JUnit rules for testing code that uses java.lang.System.
* [JUnit Toolbox](https://junit-toolbox.googlecode.com/) – Provides runners for parallel testing, a `PoolingWait` class to ease asynchronous testing, and a `WildcardPatternSuite` which allow you to specify wildcard patterns instead of explicitly listing all classes when you create a suite class.
* [junit-dataprovider](https://github.com/TNG/junit-dataprovider) – A TestNG like dataprovider (see [here](http://testng.org/doc/documentation-main.html#parameters-dataproviders)) runner for JUnit.
* [junit-quickcheck](https://github.com/pholser/junit-quickcheck) – QuickCheck-style parameter suppliers for JUnit theories. Uses [junit.contrib's version of the theories machinery](https://github.com/junit-team/junit.contrib/tree/master/theories), which respects generics on theory parameters.
* [JGiven](http://jgiven.org) - Behavior-Driven Development (BDD) for JUnit