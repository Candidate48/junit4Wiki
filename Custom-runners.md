## Third Party Runners ##

Some popular third party implementations of runners for use with `@RunWith` include:

- Spring Framework
  - [Spring TestContext Framework](http://docs.spring.io/spring/docs/current/spring-framework-reference/html/testing.html#testcontext-framework) reference manual
  - [SpringJUnit4ClassRunner](http://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/test/context/junit4/SpringJUnit4ClassRunner.html) Javadoc API
- Mockito
  - [MockitoJUnitRunner](http://javadoc.io/page/org.mockito/mockito-core/latest/org/mockito/junit/MockitoJUnitRunner.html)
- JMockit  
  - http://jmockit.org/api1x/mockit/integration/junit4/JMockit.html
- Concurrency / Test Helpers
  - [Parallel Test Runner](https://github.com/diva-e/parallel-test-runner)
  - [ConcurrentTestRunner](http://tempusfugitlibrary.org/apidocs/com/google/code/tempusfugit/concurrency/ConcurrentTestRunner.html) (Run tests [in parallel](http://tempusfugitlibrary.org/documentation/junit/parallel/))
  - [JUnit Toolbox](https://code.google.com/p/junit-toolbox/) (Run tests in parallel; also Suite and Categories with Patterns, async)
  - [IntermittentTestRunner](http://tempusfugitlibrary.org/apidocs/com/google/code/tempusfugit/concurrency/IntermittentTestRunner.html) ([run repeatedly to expose intermittent failures](http://tempusfugitlibrary.org/documentation/junit/intermittent/))
- [Hierarchical Context Runner](https://github.com/bechte/junit-hierarchicalcontextrunner/wiki) – A runner implementation that supports context hierarchies in JUnit.
- Parameterised and data-driven testing
  - [junit-dataprovider](https://github.com/TNG/junit-dataprovider/wiki) – A [TestNG](http://testng.org/doc/index.html) like dataprovider (see [here](http://testng.org/doc/documentation-main.html#parameters-dataproviders)) runner for [JUnit](https://github.com/junit-team/junit).
  - [JUnitParams](https://github.com/Pragmatists/JUnitParams) - an alternative to JUnit's `Parameterized` runner, which support test data on a per method basis
  - [ParameterizedSuite](https://github.com/PeterWippermann/parameterized-suite) - Allows to define parameters for test suites.
- [HookInstallingRunner](https://github.com/Nordstrom/JUnit-Foundation/blob/master/src/main/java/com/nordstrom/automation/junit/HookInstallingRunner.java) - This JUnit test runner implements four significant features:
  - Invocation hooks for test and configuration methods
  - Test method timeout management
  - Automatic retry of failed tests
  - Shutdown hook installation
- BDD testing - these integrate popular BDD/ATDD methodologies
  - [Cucumber Runner](https://github.com/cucumber/cucumber-jvm/blob/master/junit/src/main/java/cucumber/api/junit/Cucumber.java) - Cucumber JVM integration for JUnit, based on Gherkin specifications written in feature files
  - JBehave - [JBehave JUnit runner](https://github.com/codecentric/jbehave-junit-runner) - a Gherkin-based specification framework
  - FitNesse - [FitNesse Runner](http://fitnesse.org/FitNesse.UserGuide.WritingAcceptanceTests.RunningFromJunit)
  - [ConcordionRunner](https://github.com/concordion/concordion/blob/master/src/main/java/org/concordion/integration/junit4/ConcordionRunner.java) - the Concordion BDD framework based on Gherkin specifications written in markdown
  - [Spectrum](https://github.com/greghaskins/spectrum) - supports Specs in Jasmine/Mocha/Gherkin syntax (Java 8 required)
  - [Oleaster](https://github.com/mscharhag/oleaster) - supports Specs in Jasmine/Mocha syntax
  - [Ginkgo4jRunner](https://github.com/paulcwarren/ginkgo4j) - supports Specs in Jasmine/Mocha syntax
  - Cola tests - technically a precompiler for tests - [Cola Documentation](http://bmsantos.github.io/cola-maven-plugin/)
- [JICUnit](https://github.com/Lucas3oo/jicunit) - A JUnit runner in the JEE container for in-container testing similar to JUnitEE and Jakarta Cactus, both which are not developed any more.
- [JUnit Browser Runner](https://github.com/dukescript/junit-browser-runner) - A JUnit runner that executes your tests in a Browser using [bck2brwsr](http://wiki.apidesign.org/wiki/Bck2Brwsr).