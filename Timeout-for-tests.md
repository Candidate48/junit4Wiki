Tests that 'runaway' or take too long, can be automatically failed.  There are two options for implementing this behaviour:

### Timeout parameter on @Test Annotation (applies to test method)
You can optionally specify timeout in milliseconds to cause a test method to fail if it takes longer than that number of milliseconds.  If the time limit is exceeded, the the failure is triggered by a `TimeoutException` being thrown:

				@Test(timeout=1000)
				public void testWithTimeout() {
				  ...
				}


### Timeout Rule (applies to entire test class)
The Timeout Rule applies the same timeout to all test methods in a class:



				 public static class HasGlobalTimeout {
						public static String log;
				 
						@Rule
						public MethodRule globalTimeout= new Timeout(20);
				 
						@Test
						public void testInfiniteLoop1() {
								log+= "ran1";
								for (;;) {
								}
						}
				 
						@Test
						public void testInfiniteLoop2() {
								log+= "ran2";
								for (;;) {
								}
						}
				 }
