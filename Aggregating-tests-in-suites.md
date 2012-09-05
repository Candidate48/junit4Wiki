Using `Suite` as a runner allows you to manually build a suite containing tests from many classes. It is the JUnit 4 equivalent of the JUnit 3.8.x `static Test suite()` method. To use it, annotate a class with `@RunWith(Suite.class)` and `@SuiteClasses(TestClass1.class, ...)`. When you run this class, it will run all the tests in all the suite classes.

## Example
The  class below is a  placeholder for the suite annotations, no other implementation is required. Note the `@RunWith` annotation, which specifies that the JUnit 4 test runner to use is `org.junit.runners.Suite` for running this particular test class. This works in conjunction with the @Suite annotation, which tells the Suite runner which test classes to include in this suite and in which order.

	import org.junit.runner.RunWith;
	import org.junit.runners.Suite;
	 
	@RunWith(Suite.class)
	@Suite.SuiteClasses({
	  TestFeatureLogin.class,
	  TestFeatureLogout.class,
	  TestFeatureNavigate.class,
	  TestFeatureUpdate.class
	})
	 
	public class FeatureTestSuite {
		// the class remains empty, 
		// used only as a holder for the above annotations
	}

