The custom runner `Parameterized` implements parameterized tests. When running a parameterized test class, instances are created for the cross-product of the test methods and the test data elements.

For example, to test a Fibonacci function, write:
```java

import static org.junit.Assert.assertEquals;

import java.util.Arrays;
import java.util.Collection;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.junit.runners.Parameterized;
import org.junit.runners.Parameterized.Parameters;

@RunWith(Parameterized.class)
public class FibonacciTest {
    @Parameters
    public static Collection<Object[]> data() {
        return Arrays.asList(new Object[][] {     
                 { 0, 0 }, { 1, 1 }, { 2, 1 }, { 3, 2 }, { 4, 3 }, { 5, 5 }, { 6, 8 }  
           });
    }

    private int fInput;

    private int fExpected;

    public FibonacciTest(int input, int expected) {
        this.fInput = input;
        this.fExpected = expected;
    }

    @Test
    public void test() {
        assertEquals(fExpected, Fibonacci.compute(fInput));
    }
}
```

```java
public class Fibonacci {
    public static int compute(int n) {
    	int result = 0;
    	
        if (n <= 1) { 
        	result = n; 
        } else { 
        	result = compute(n - 1) + compute(n - 2); 
        }
        
        return result;
    }
}
```
	 
Each instance of FibonacciTest will be constructed using the two-argument constructor and the data values in the `@Parameters` method.

## Using @Parameter for Field injection instead of Constructor

It is also possible to inject data values directly into fields without needing a constructor using the @Parameter annotation, like so:

```java
import static org.junit.Assert.assertEquals;

import java.util.Arrays;
import java.util.Collection;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.junit.runners.Parameterized;
import org.junit.runners.Parameterized.Parameter;
import org.junit.runners.Parameterized.Parameters;

@RunWith(Parameterized.class)
public class FibonacciTest {
    @Parameters
    public static Collection<Object[]> data() {
        return Arrays.asList(new Object[][] {
                 { 0, 0 }, { 1, 1 }, { 2, 1 }, { 3, 2 }, { 4, 3 }, { 5, 5 }, { 6, 8 }  
           });
    }

    @Parameter // first data value (0) is default
    public /* NOT private */ int fInput;

    @Parameter(1)
    public /* NOT private */ int fExpected;

    @Test
    public void test() {
        assertEquals(fExpected, Fibonacci.compute(fInput));
    }
}

public class Fibonacci {
    ...
}
```

This currently only works for public fields (see https://github.com/junit-team/junit/pull/737).

## Tests with single parameter

(Since 4.12-beta-3)

If your test needs a single parameter only, you don't have to wrap it with an array. Instead you can provide an Iterable or an array of objects.

```java
@Parameters
public static Iterable<? extends Object> data() {
    return Arrays.asList("first test", "second test");
}
```

or

```java
@Parameters
public static Object[] data() {
    return new Object[] { "first test", "second test" };
}
```

## Identify Individual test cases

In order to easily identify the individual test cases in a Parameterized test, you may provide a name using the @Parameters annotation. This name is allowed to contain placeholders that are replaced at runtime:

- `{index}`: the current parameter index
- `{0}, {1}, …`: the first, second, and so on, parameter value. NOTE: single quotes `'` should be escaped as two single quotes `''`.

## Example
```java
import static org.junit.Assert.assertEquals;

import java.util.Arrays;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.junit.runners.Parameterized;
import org.junit.runners.Parameterized.Parameters;

@RunWith(Parameterized.class)
public class FibonacciTest {

    @Parameters(name = "{index}: fib({0})={1}")
    public static Iterable<Object[]> data() {
        return Arrays.asList(new Object[][] { 
                 { 0, 0 }, { 1, 1 }, { 2, 1 }, { 3, 2 }, { 4, 3 }, { 5, 5 }, { 6, 8 }
           });
    }

    private int input;
    private int expected;

    public FibonacciTest(int input, int expected) {
        this.input = input;
        this.expected = expected;
    }

    @Test
    public void test() {
        assertEquals(expected, Fibonacci.compute(input));
    }
}

public class Fibonacci {
    ...
}
```

In the example given above, the Parameterized runner creates names like [3: fib(3)=2]. If you don't specify a name, the current parameter index will be used by default.

## IDE Bug (Eclipse)
If using the `name` annotation param and one of the inputs has a rounded bracket, e.g. `@Parameters(name = "test({index})")`, then the name gets truncated in Eclipse versions prior to 4.4 (Luna). See https://bugs.eclipse.org/bugs/show_bug.cgi?id=102512.

Before the Mars M4 release Eclipse wasn't able to run individual test subtrees, such as the ones create by the Parameterized runner.
See http://blog.moritz.eysholdt.de/2014/11/new-eclipse-junit-feature-run-subtrees.html and https://bugs.eclipse.org/bugs/show_bug.cgi?id=443498.

## See also
* As an alternative to parameterized tests you can also use the plugin [JUnitParams](https://github.com/Pragmatists/JUnitParams)
* If you want to define the parameters for your tests at the tests' `Suite`, you can use the `ParameterizedSuite` runner that is available in [a separate library](https://github.com/PeterWippermann/parameterized-suite).