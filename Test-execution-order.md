#Test execution order

By design, JUnit does not specify the execution order of test method invocations. Until now, the methods were simply invoked in the order returned by the reflection API. However, using the JVM order is unwise since the Java platform does not specify any particular order, and in fact JDK 7 returns a more or less random order. Of course, well-written test code would not assume any order, but some does, and a predictable failure is better than a random failure on certain platforms.

From version 4.11, JUnit will by default use a deterministic, but not predictable, order `(MethodSorters.DEFAULT)`. To change the test execution order simply annotate your test class using `@FixMethodOrder` and specify one of the available MethodSorters:

`@FixMethodOrder(MethodSorters.JVM)`: Leaves the test methods in the order returned by the JVM. This order may vary from run to run.

`@FixMethodOrder(MethodSorters.NAME_ASCENDING)`: Sorts the test methods by method name, in lexicographic order.