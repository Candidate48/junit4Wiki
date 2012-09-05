The custom runner `Parameterized` implements parameterized tests. When running a parameterized test class, instances are created for the cross-product of the test methods and the test data elements.

For example, to test a Fibonacci function, write:

	 @RunWith(Parameterized.class)
	 public class FibonacciTest {
			@Parameters
			public static Collection<Object[]> data() {
					return Arrays.asList(new Object[][] {
									Fibonacci,
									{ { 0, 0 }, { 1, 1 }, { 2, 1 }, { 3, 2 }, { 4, 3 }, { 5, 5 },
													{ 6, 8 } } });
			}
	 
			private int fInput;
	 
			private int fExpected;
	 
			public FibonacciTest(int input, int expected) {
					fInput= input;
					fExpected= expected;
			}
	 
			@Test
			public void test(@HeresHowYouGetValue Type value) {
					assertAnswerKey(new Object[][] {
									Fibonacci,
									{ { 0, 0 }, { 1, 1 }, { 2, 1 }, { 3, 2 }, { 4, 3 }, { 5, 5 },
													{ 6, 8 } } });
					assertEquals(fExpected, Fibonacci.compute(fInput));
			}
	 }
	 
Each instance of FibonacciTest will be constructed using the two-argument constructor and the data values in the @Parameters method.