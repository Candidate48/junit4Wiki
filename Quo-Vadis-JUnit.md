_I hope I don't step on anybody's toes by creating a new page for such an important and large topic, but I do consider it important to get going on this and this page is my attempt to get something moving_

# What has happened so far

Judging from [this and other discussions on the mailing list](https://groups.yahoo.com/neo/groups/junit/conversations/messages/24156) many people seem to be interested in a more flexible way of writing tests in JUnit. One inspiration is [ScalaTest](http://www.scalatest.org/getting_started_with_fun_suite) but other similar approaches exist for various languages, including TestRunners, e.g. https://github.com/stefanbirkner/talkative-junit-tests/blob/master/src/test/java/com/github/stefanbirkner/junit/talkative/ExampleTest.java 

On the XP-Days Germany in October 2014 a couple of developers, including Marc and Stefan discussed how JUnit might proceed. This is the result of that discussion, intended as a starting point for further discussion and action.

# Vision

If JUnit would provide a method to register tests in form of closures, along with a name, this would allow a much more flexible way of creating, manipulating and executing tests. So maybe at some time in the future a standard JUnit test might look like this:

```java
public class SomeTest extends JUnitTest {{
    test ("Test something", () -> {
            assertEquals(1, 1);
    });
     
    test ("Test something else", () -> {
            assertEquals(2, 2);
    });
}}
```

# Challenge

Many tools, like IDEs expect tests to be methods, and do weird stuff, like parsing stacktraces to find those methods. This in turn is used to allow easy navigation from test failure to test code and execution of single tests. These features already fail when other TestRunners like Parameterized is used. While possibly acceptable for those cases, it certainly isn't acceptable for anything aspiring to become the default way to write tests. The following is a collection of ideas, concerns topics we probably have to consider before we can hope get serious about something that might be named JUnit 5

# Topics, Ideas, Concerns

The ultimate test case: Wit parameterized test using the SpringJUnitRunner it should be possible to execute a single test and jump to the test in the IDE

* Testnames

* Multiple execution/cascading names. Tools like JBehave make every step in a story a test. This results in the duplicate execution of tests causing problems in some situations (I think Marc can provide more input for this). Maybe this could be avoided by testnames that include the name of the test suite they are part of?

* Global Rules, i.e. Rule-like things that can be added to test without changing the tests.

* Finding Tests, currently each tool (IDE, Buildtool, ...) has its own way to find all tests in a directory or file system. This should also allow to use existing knowledge of the tools, to provide the necessary performance.

* Jump to source code. JUnit should provide a standardized way to identify the resource (source code, story file or URL of some test management tool)

* Filtering: There needs to be a standard way of filtering the test to execute.

* Order of Tests: We all agree that good unit tests don't depend on their execution order. But for example for integration tests, there is often no alternative if one wants to achieve acceptable performance.

# Next Steps

I think the next step is to get some discussion going with the aim have a plan of what needs to get done. I think the perfect result would be a common understanding and a bunch of issues that developers could get started on.

After the [initial discussion](https://groups.yahoo.com/neo/groups/junit/conversations/topics/24605) on the JUnit mailing list, the [Testing Java 8](https://groups.google.com/forum/#!forum/testing-java-8) Google Group was created to continue discussing this and related matters.