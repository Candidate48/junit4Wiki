# Creating a New Test Case

Here is a template for writing JUnit4-style tests:

    package com.example.foo;

    import static org.junit.Assert.assertEquals;

    import org.junit.Test;
    import org.junit.runner.RunWith;
    import org.junit.runners.JUnit4;

    /**
     * Tests for {@link Foo}.
     *
     * @author user@example.com (John Doe)
     */
    @RunWith(JUnit4.class)
    public class FooTest {

      @Test
      public void thisAlwaysPasses() {
      }

      @Test
      @Ignore
      public void thisIsIgnored() {
      }
    }


Notes:
* All test methods are annotated with @Test. Unlike JUnit3 tests, you do not need to prefix the method name with "test" (and usually don't)
* Do not have your test classes extend `junit.framework.TestCase` (directly or indirectly).
Usually, tests with JUnit4 do not need to extend anything (which is good, since Java does not support multiple inheritance)
* Do not use any classes in `junit.framework` or `junit.extensions`
