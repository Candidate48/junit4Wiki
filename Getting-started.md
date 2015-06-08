This small example shows you how to write a unit test. You need to have a JDK installed and a text editor. (In general it is recommended to use a build tool for building your software and running the tests.)

## Preparation

Create a new folder `junit-example` and download the current `junit-4.XX.jar` from JUnit's [release page](https://github.com/junit-team/junit/releases) and [Hamcrest](http://search.maven.org/remotecontent?filepath=org/hamcrest/hamcrest-core/1.3/hamcrest-core-1.3.jar) to this folder. Change to the folder `junit-example`. All files are created within this folder and all commands are executed there, too.

## Create the class under test

Create a new file `Calculator.java` and copy the following code to this file.

```java
public class Calculator {
  public int evaluate(String expression) {
    int sum = 0;
    for (String summand: expression.split("\\+"))
      sum += Integer.valueOf(summand);
    return sum;
  }
}
```

Now compile this class:

    javac Calculator.java

The Java compiler creates a file `Calculator.class`.

## Create a test

Create the file `CalculatorTest.java` and copy the following code to this file.

```java
import static org.junit.Assert.assertEquals;
import org.junit.Test;

public class CalculatorTest {
  @Test
  public void evaluatesExpression() {
    Calculator calculator = new Calculator();
    int sum = calculator.evaluate("1+2+3");
    assertEquals(6, sum);
  }
}
```
Compile the test:

    javac -cp .:junit-4.XX.jar CalculatorTest.java

The Java compiler creates a file `CalculatorTest.class`.

## Run the test

Run the test from the command line:

    java -cp .:junit-4.XX.jar:hamcrest-core-1.3.jar org.junit.runner.JUnitCore CalculatorTest

The output is

    JUnit version 4.12
    .
    Time: 0,006
    
    OK (1 test)

The single `.` means that one test has been run and the `OK` in the last line tells you that your test is successful.

## Let the test fail

Modify `Calculator.java` in order to get a failing test. Replace the line

    sum += Integer.valueOf(summand);

with

    sum -= Integer.valueOf(summand);

and recompile the class.

    javac Calculator.java

Run the test again:

    java -cp .:junit-4.XX.jar:hamcrest-core-1.3.jar org.junit.runner.JUnitCore CalculatorTest

Now the test fails and the output is

    JUnit version 4.12
    .E
    Time: 0,007
    There was 1 failure:
    1) evaluatesExpression(CalculatorTest)
    java.lang.AssertionError: expected:<6> but was:<-6>
      at org.junit.Assert.fail(Assert.java:88)
      ...
    
    FAILURES!!!
    Tests run: 1,  Failures: 1

JUnit tells you which test failed (`evaluatesExpression(CalculatorTest)`) and what went wrong:

    java.lang.AssertionError: expected:<6> but was:<-6>