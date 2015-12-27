Tests that 'runaway' or take too long, can be automatically failed.  There are two options for implementing this behaviour:

### Timeout parameter on @Test Annotation (applies to test method)
You can optionally specify timeout in milliseconds to cause a test method to fail if it takes longer than that number of milliseconds.  If the time limit is exceeded, then the failure is triggered by an `Exception` being thrown:

```java
@Test(timeout=1000)
public void testWithTimeout() {
  ...
}
```

This is implemented by running the test method in a separate test. If the test runs longer than the allotted timeout, the test will fail and JUnit will interrupt the thread running the test, so if the test is running an interrupt able operation, the thread running the test will exit (if the test is in an infinite loop, the thread running the test will run forever).

### Timeout Rule (applies to all test cases in the test class)
The Timeout Rule applies the same timeout to all test methods in a class, and will [currently](https://github.com/junit-team/junit/issues/1126) take precedence over any timeout parameter on an individual Test annotation.:

```java
public class HasGlobalTimeout {
    public static String log;

    @Rule
    public Timeout globalTimeout = Timeout.seconds(10); // 10 seconds max per method tested

    @Test
    public void testInfiniteLoop1() throws Exception {
        log += "ran1";
        Thread.sleep(100_000); // sleep for 100 seconds
    }

    @Test
    public void testInfiniteLoop2() throws Exception {
        log += "ran2";
        Thread.sleep(100_000); // sleep for 100 seconds
    }
}
```

The timeout specified in the `Timeout` rule applies to the entire test fixture, including any `@Before` or `@After` methods. If the test method is in an infinite loop (or is otherwise not responsive to interrupts) then `@After` methods will not be called.