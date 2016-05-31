## Third Party Runners ##

Some popular third party implementations of runners for use with `@RunWith` include:

- Spring Framework
 - [Spring TestContext Framework](http://docs.spring.io/spring/docs/current/spring-framework-reference/html/testing.html#testcontext-framework) reference manual
 - [SpringJUnit4ClassRunner](http://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/test/context/junit4/SpringJUnit4ClassRunner.html) Javadoc API
- Mockito
 - [MockitoJUnitRunner](http://docs.mockito.googlecode.com/hg/latest/org/mockito/runners/MockitoJUnitRunner.html)
- JMockit  
 - http://jmockit.org/api1x/mockit/integration/junit4/JMockit.html
- Concordion
 - [ConcordionRunner](https://github.com/concordion/concordion/blob/master/src/main/java/org/concordion/integration/junit4/ConcordionRunner.java)
- [Cucumber Runner](https://github.com/cucumber/cucumber-jvm/blob/master/junit/src/main/java/cucumber/api/junit/Cucumber.java)
- Concurrency / Test Helpers
 - [ConcurrentTestRunner](http://tempusfugitlibrary.org/apidocs/com/google/code/tempusfugit/concurrency/ConcurrentTestRunner.html) (Run tests [in parallel](http://tempusfugitlibrary.org/documentation/junit/parallel/))
 - [JUnit Toolbox](https://code.google.com/p/junit-toolbox/) (Run tests in parallel; also Suite and Categories with Patterns, async)
 - [IntermittentTestRunner](http://tempusfugitlibrary.org/apidocs/com/google/code/tempusfugit/concurrency/IntermittentTestRunner.html) ([run repeatedly to expose intermittent failures](http://tempusfugitlibrary.org/documentation/junit/intermittent/))
- [Hierarchical Context Runner](https://github.com/bechte/junit-hierarchicalcontextrunner/wiki) – A runner implementation that supports context hierarchies in JUnit.
- [junit-dataprovider](https://github.com/TNG/junit-dataprovider/wiki) – A [TestNG](http://testng.org/doc/index.html) like dataprovider (see [here](http://testng.org/doc/documentation-main.html#parameters-dataproviders)) runner for [JUnit](https://github.com/junit-team/junit).
- JBehave 
  - [JBehave JUnit runner](https://github.com/codecentric/jbehave-junit-runner)
- FitNesse
  - [FitNesse Runner](http://fitnesse.org/FitNesse.UserGuide.WritingAcceptanceTests.RunningFromJunit)
- [JICUnit](https://github.com/Lucas3oo/jicunit) - A JUnit runner in the JEE container for in-container testing similar to JUnitEE and Jakarta Cactus, both which are not developed any more.
- [Junit Browser Runner](https://github.com/dukescript/junit-browser-runner) - A JUnit runner that executes your tests in a Browser using [bck2brwsr](http://wiki.apidesign.org/wiki/Bck2Brwsr).