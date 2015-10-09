This small example shows you how to write and run a unit test with [Ant](http://ant.apache.org/). You need to have Ant installed and a text editor.

## Preparation

Create a new folder `junit-example` and a sub-folder `lib`. Download the current [JUnit](https://github.com/junit-team/junit/releases/download/r4.12/junit-4.12.jar) and [Hamcrest](http://search.maven.org/remotecontent?filepath=org/hamcrest/hamcrest-core/1.3/hamcrest-core-1.3.jar) into the sub-folder `lib`. 

## Build file

Create the build file `build.xml` in the `junit-example` folder.

```ant
<project name="junit-example">
  <property name="main.build.dir" value="build/main"/>
  <property name="main.src.dir" value="src/main/java"/>
  <property name="test.build.dir" value="build/test"/>
  <property name="test.src.dir" value="src/test/java"/>

  <path id="classpath.test">
    <pathelement location="lib/junit-4.12.jar"/>
    <pathelement location="lib/hamcrest-core-1.3.jar"/>
    <pathelement location="${main.build.dir}"/>
  </path>

  <target name="compile">
    <mkdir dir="${main.build.dir}"/>
    <javac srcdir="${main.src.dir}" destdir="${main.build.dir}" includeantruntime="false"/>
  </target>

  <target name="test-compile" depends="compile">
    <mkdir dir="${test.build.dir}"/>
    <javac srcdir="${test.src.dir}" destdir="${test.build.dir}" includeantruntime="false">
        <classpath refid="classpath.test"/>
    </javac>
  </target>

  <target name="test" depends="test-compile">
    <junit printsummary="on" haltonfailure="yes" fork="true">
        <classpath>
          <path refid="classpath.test"/>
          <pathelement location="${test.build.dir}"/>
        </classpath>
        <formatter type="brief" usefile="false" />
        <batchtest>
            <fileset dir="${test.src.dir}" includes="**/*Test.java" />
        </batchtest>
    </junit>
  </target>
</project>
```

## Create the class under test

Create a sub-folder `src/main/java` and a new file `Calculator.java` within this sub-folder. Copy the following code to this file.

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

## Create a test

Create a sub-folder `src/test/java` and a new file `CalculatorTest.java` within this sub-folder. Copy the following code to this file.

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

## Run the test

Run the test from the command line.

    ant test

The output is

    Buildfile: /home/kent/junit-example/build.xml

    compile:
        [mkdir] Created dir: /home/kent/junit-example/build/main
        [javac] Compiling 1 source file to /home/you/junit-example/build/main

    test-compile:
        [mkdir] Created dir: /home/kent/junit-example/build/test
        [javac] Compiling 1 source file to /home/you/junit-example/build/test

    test:
        [junit] Running CalculatorTest
        [junit] Testsuite: CalculatorTest
        [junit] Tests run: 1, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 0,014 sec
        [junit] Tests run: 1, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 0,014 sec
        [junit] 

    BUILD SUCCESSFUL
    Total time: 0 seconds

The second last line tells you that your test is successful.

## Let the test fail

Modify `Calculator.java` in order to get a failing test. Replace the line

    sum += Integer.valueOf(summand);

with

    sum -= Integer.valueOf(summand);

and run the test again.

    ant test

Now the test fails and the last lines of the output are

    [junit] Tests run: 1, Failures: 1, Errors: 0, Skipped: 0, Time elapsed: 0,017 sec
    [junit] 
    [junit] Testcase: evaluatesExpression(CalculatorTest):	FAILED
    [junit] expected:<6> but was:<-6>
    [junit] junit.framework.AssertionFailedError: expected:<6> but was:<-6>
    [junit] 	at CalculatorTest.evaluatesExpression(Unknown Source)
    [junit] 
    [junit] 

    BUILD FAILED
    /home/kent/junit-example/build.xml:26: Test CalculatorTest failed


JUnit tells you which test failed (`CalculatorTest.evaluatesExpression`) and what went wrong:

    expected:<6> but was:<-6>