Tests that 'runaway' or take too long, can be automatically failed.  There are two options for implementing this behavior:

### Timeout parameter on @Test Annotation (applies to test method)
You can optionally specify timeout in milliseconds to cause a test method to fail if it takes longer than that number of milliseconds.  If the time limit is exceeded, then the failure is triggered by an `Exception` being thrown:

```java
@Test(timeout=1000)
public void testWithTimeout() {
  ...
}
```

This is implemented by running the test method in a separate thread. If the test runs longer than the allotted timeout, the test will fail and JUnit will interrupt the thread running the test. If a test times out while executing an interruptible operation, the thread running the test will exit (if the test is in an infinite loop, the thread running the test will run forever, while other tests continue to execute).

### Timeout Rule (applies to all test cases in the test class)
The Timeout Rule applies the same timeout to all test methods in a class, and will [currently](https://github.com/junit-team/junit/issues/1126) execute in addition to any timeout specified by the `timeout` parameter on an individual Test annotation.:

```java
import org.junit.Rule;
import org.junit.Test;
import org.junit.rules.Timeout;

public class HasGlobalTimeout {
    public static String log;
    private final CountDownLatch latch = new CountDownLatch(1);

    @Rule
    public Timeout globalTimeout = Timeout.seconds(10); // 10 seconds max per method tested

    @Test
    public void testSleepForTooLong() throws Exception {
        log += "ran1";
        TimeUnit.SECONDS.sleep(100); // sleep for 100 seconds
    }

    @Test
    public void testBlockForever() throws Exception {
        log += "ran2";
        latch.await(); // will block 
    }
}
```

The timeout specified in the `Timeout` rule applies to the entire test fixture, including any `@Before` or `@After` methods. If the test method is in an infinite loop (or is otherwise not responsive to interrupts) then `@After` methods will not be called.

### Global Timeout Management with JUnit Foundation

[JUnit Foundation](https://github.com/Nordstrom/JUnit-Foundation) provides a timeout management feature that enables you to specify a configurable global timeout interval. The timeout behavior is provided by the **JUnit** framework via the `timeout` parameter of the **`@Test`** annotation. If no `timeout` parameter has been specified, or if the configured global timeout specifies a longer interval, **JUnit Foundation** overrides the **`@Test`** annotation with a mutable replacement that specifies the configured `timeout` parameter.

Timeout management is applied automatically by the **JUnit Foundation** Java agent, activated by setting the `TEST_TIMEOUT` configuration option to the desired default test timeout interval in milliseconds. This timeout specification is applied to every test method that doesn't explicitly specify a longer interval.