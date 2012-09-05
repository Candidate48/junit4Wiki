## IDE's
Netbeans, Eclipse and IntelliJ Idea have native graphical test runners built in.

## Console based Test runner
JUnit provides tools to define the suite to be run and to display its results. To run tests and see the results on the console, run this from a Java program:

    org.junit.runner.JUnitCore.runClasses(TestClass1.class, ...);

or this from the command line, with both your test class and junit on the classpath:

    java org.junit.runner.JUnitCore TestClass1 [...other test classes...]

This usage is documented further here: http://junit.org/apidocs/junit/textui/TestRunner.html

## Using older runners with Adapter
`JUnit4Adapter` enables running the new JUnit4 tests using the old JUnit runners.  To us it add the following  to a test class:

      public static Test suite() {
        return new JUnit4TestAdapter(AdditionAllTests.class);
      }
