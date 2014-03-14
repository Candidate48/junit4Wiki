Tests that 'runaway' or take too long, can be automatically failed.  There are two options for implementing this behaviour:

### Timeout parameter on @Test Annotation (applies to test method)
You can optionally specify timeout in milliseconds to cause a test method to fail if it takes longer than that number of milliseconds.  If the time limit is exceeded, the the failure is triggered by an `Exception` being thrown:

```java
@Test(timeout=1000)
public void testWithTimeout() {
  ...
}
```

### Timeout Rule (applies to entire test class)
The Timeout Rule applies the same timeout to all test methods in a class:

```java
public class HasGlobalTimeout {
    public static String log;

    @Rule
    public Timeout globalTimeout = new Timeout(10000); // 10 seconds max per method tested

    @Test
    public void testInfiniteLoop1() {
        log += "ran1";
        for (;;) {
        }
    }

    @Test
    public void testInfiniteLoop2() {
        log += "ran2";
        for (;;) {
        }
    }
}
```