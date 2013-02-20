Theories

More flexible and expressive assertions, combined with the ability to state assumptions clearly, lead to a new kind of statement of intent, which we call a "Theory". A test captures the intended behavior in one particular scenario. A theory captures some aspect of the intended behavior in possibly infinite numbers of potential scenarios. For example:
```java
@RunWith(Theories.class)
public class UserTest {
    @DataPoint
    public static String GOOD_USERNAME = "optimus";
    @DataPoint
    public static String USERNAME_WITH_SLASH = "optimus/prime";

    @Theory
    public void filenameIncludesUsername(String username) {
        assumeThat(username, not(containsString("/")));
        assertThat(new User(username).configFileName(), containsString(username));
    }
}
```

This makes it clear that the user's filename should be included in the config file name, only if it doesn't contain a slash. Another test or theory might define what happens when a username does contain a slash.

UserTest will attempt to run filenameIncludesUsername on every compatible DataPoint defined in the class. If any of the assumptions fail, the data point is silently ignored. If all of the assumptions pass, but an assertion fails, the test fails.

The support for Theories has been absorbed from the Popper project, and more complete documentation can be found from that projects documentation archived here: http://web.archive.org/web/20071012143326/popper.tigris.org/tutorial.html
(also reproduced below).

A paper written on theories is here http://web.archive.org/web/20110608210825/http://shareandenjoy.saff.net/tdd-specifications.pdf

Defining general statements in this way can jog the developer's memory about other potential data points and tests, also allows automated tools to search for new, unexpected data points that expose bugs.

## Documentation from defunct Popper project
Popper extends JUnit to allow you to specify theories, general statements about your code's behavior that may be true over infinite sets of input values. For a detailed description of why you might want to do this, see our paper. If you just want to try it out and get started, here's the place.

First, if you haven't already, download the latest Popper. Popper should work with any version of JUnit between 4.0 and 4.3, and Java 5 and above.

Put Popper and JUnit on your classpath.

Now, let's start with a simple test class for a type that performs arithmetic on numbers of dollars:
```java
public class DollarTest {
    @Test
    public void multiplyByAnInteger() {
        assertThat(new Dollar(5).times(2).getAmount(), is(10));
    }
}
```

This demonstrates the syntax of JUnit 4 tests written with Popper's `assertThat` syntax, which is lovingly stolen from Hamcrest. If the `@Test` syntax is new to you, you may want to quickly get up to speed on JUnit 4. If the convenient `assertThat` assertion syntax is new, you may want to get up to speed on Hamcrest. (You'll need to add some imports. Eclipse can take care of most of them for you, but here's the whole list)

Go ahead and get the test above to pass. I especially suggest that you cheat by always returning 10 from getAmount.

Now, we'll see how Popper extends JUnit to allow the specification and verification of general properties. First, give Dollar test a new superclass:
```java
import net.saff.theories.api.TheoryContainer;

public class DollarTest extends TheoryContainer {
    // ...
    // Next, add a theory to the test class:

    @Theory
    public void multiplyIsInverseOfDivide(int amount, int m) {
        assumeThat(m, not(0));
        assertThat(new Dollar(amount).times(m).divideBy(m).getAmount(), is(amount));
    }
```
You'll have to add a divideBy method to Dollar in order to get the class to compile. This theory expresses a general truth about currency multiplication and division: one is the inverse of the other. By adding two parameters to the method, and adding the assumption that m is not zero, you've specified that this theory should hold true for any value of amount and all non-zero values of m.

Go ahead and run the tests, and you'll notice two things:

- Your multiplyByAnInteger test passes as before.
- multiplyIsInverseOfDivide fails, with the message "Never found parameters that satisfied method."

The Popper runner does not automatically provide potential values for a theory. It can take a long time between being able to assert a general principle, and actually making it work with any conceivable input. Because of this, Popper expects to only run theories on a set of accepted data points, which allows you to incrementally build up a set of inputs for which you know the theory passes, until you feel confident that the theory is universally true.

By default, Popper assumes that all public fields of a test class are accepted data points. For example, add the following constants to `DollarTest`:
```java
public static int TWO = 2;
public static int FIVE = 5;
public static int TEN = 10;
```

Now the theory will probably fail, telling you which inputs caused the failure. Fix your implementations of times and divideBy, and the theory should pass.

To customize how Popper finds accepted data points, you can use parameter suppliers. One parameter supplier comes with Popper by default, which allows you to specify inline a set of acceptable integer inputs to a theory:
```java
@Theory
public void multiplyIsInverseOfDivideWithInlineDataPoints(
        @TestedOn(ints = {0, 5, 10}) int amount,
        @TestedOn(ints = {0, 1, 2}) int m
) {
    assumeThat(m, not(0));
    assertThat(new Dollar(amount).times(m).divideBy(m).getAmount(), is(amount));
}
```

This theory ignores the public fields of DollarTest, and tests with every combination of 0, 5, and 10 for amount, and 0, 1, and 2 for m. Notice that even though 0 is tried as a value for m, it does not trigger an arithmetic exception or failure: values that violate assumptions are quietly ignored.

You can extend Popper by providing your own parameter supplier. For example, here is a supplier for values between two integers, and an annotation that references it:
```java
@Retention(RetentionPolicy.RUNTIME)
@ParametersSuppliedBy(BetweenSupplier.class)
public @interface Between {
    int first();

    int last();
}

public static class BetweenSupplier extends ParameterSupplier {
    @Override
    public List getValues(Object test, ParameterSignature sig) {
        Between annotation = (Between) sig.getSupplierAnnotation();

        ArrayList list = new ArrayList();
        for (int i = annotation.first(); i <= annotation.last(); i++)
            list.add(i);
        return list;
    }
}
```

With this supplier defined, you can accept data points as ranges:
```java
@Theory
public void multiplyIsInverseOfDivideWithInlineDataPoints(
        @Between(first = -100, last = 100) int amount,
        @Between(first = -100, last = 100) int m
) {
    assumeThat(m, not(0));
    assertThat(new Dollar(amount).times(m).divideBy(m).getAmount(), is(amount));
}
```

The paper refers to a capacity for automatically generating stubs to pass as object parameters to theories.