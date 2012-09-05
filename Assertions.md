JUnit provides overloaded assertion methods for all primitive types and Objects and arrays (of primitives or Objects).  The parameter order is expected value followed by actual value.  Optionally the first parameter can be a String message that is output on failure.
There is a slightly different assertion, `assertThat` that has parameters of the optional failure message, the actual value, and a `Matcher` object.  Note that expected and actual are reversed compared to the other assert methods.

## Examples

A representative of each assert method is shown.

	import org.junit.Test;
	
	public class AssertTests {
		@Test
		public void testassertArrayEquals() {
			byte[] expected = "trial".getBytes();
			byte[] actual = "trial".getBytes();
			org.junit.Assert.assertArrayEquals("failure - byte arrays not same", expected, actual);
		}
	
		@Test
		public void testassertEquals() {
			String expected = "trial";
			String actual = "trial";
			org.junit.Assert.assertEquals("failure - strings not same", expected, actual);
		}
	
		@Test
		public void testassertFalse() {
			org.junit.Assert.assertFalse("failure - should be false", false);
		}
	}