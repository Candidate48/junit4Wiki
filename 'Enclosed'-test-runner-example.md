
# Enclosed TestRunner usage #
Example of using ``Enclosed`` TestRunner.

We want to test this domain class; testing Equals, HashCode, Serilizable, Comparable, and the Builders.   This can be simply done using the testhelpers from https://github.com/chas66/TestHelpers

Usually we would need a subclass of each abstract test, however with the `Enclosed` runner, they can all be static inner classes of the same test case class.

Here's the domain class to test.

# Class To Test #

		package abstractions.domain;

		import java.io.Serializable;

		import com.google.common.collect.ComparisonChain;

		public class Address implements Serializable, Comparable<Address> {

			private static final long serialVersionUID = 1L;
			private final String address1;
			private final String city;
			private final String state;
			private final String zip;

			private Address(Builder builder) {
				this.address1 = builder.address1;
				this.city = builder.city;
				this.state = builder.state;
				this.zip = builder.zip;
			}

			public String getAddress1() {
				return address1;
			}

			public String getCity() {
				return city;
			}

			public String getState() {
				return state;
			}

			public String getZip() {
				return zip;
			}

			@Override
			public int hashCode() {
				return com.google.common.base.Objects.hashCode(getAddress1(), getCity(), getCity(), getState(), getZip());
			}

			@Override
			public String toString() {
				return com.google.common.base.Objects.toStringHelper(this).addValue(getAddress1()).addValue(getCity()).addValue(getState()).addValue(getZip()).toString();
			}

			public static class Builder {

				private String address1;
				private String city;
				private String state;
				private String zip;

				public Builder address1(String address1) {
					this.address1 = address1;
					return this;
				}

				public Address build() {
					return new Address(this);
				}

				public Builder city(String city) {
					this.city = city;
					return this;
				}

				public Builder state(String state) {
					this.state = state;
					return this;
				}

				public Builder zip(String zip) {
					this.zip = zip;
					return this;
				}
			}
		}

# Tests #		
And here are the test cases, implemented as inner classes, using the ``Enclosed`` runner:

		package abstractions.domain;

		import static org.hamcrest.Matchers.is;
		import static org.junit.Assert.assertThat;

		import java.io.Serializable;

		import org.junit.Before;
		import org.junit.Test;
		import org.junit.experimental.runners.Enclosed;
		import org.junit.runner.RunWith;

		import testhelpers.ComparabilityTestCase;
		import testhelpers.EqualsHashCodeTestCase;
		import testhelpers.SerializabilityTestCase;

		/**
		 * The Class AddressTest.
		 */
		@RunWith(Enclosed.class)
		public class AddressTest {

			/**
			 * The Class AddressComparabilityTest.
			 */
			public static class AddressComparabilityTest extends ComparabilityTestCase<Address> {

				@Override
				protected Address createEqualInstance() throws Exception {
					return new Address.Builder().address1("2802 South Havana Street").city("Aurora").state("CO").zip("80014").build();
				}

				@Override
				protected Address createGreaterInstance() throws Exception {
					return new Address.Builder().address1("9839 Carlisle Boulevard NE").city("Albuquerque").state("NM").zip("87110").build();
				}

				@Override
				protected Address createLessInstance() throws Exception {
					return new Address.Builder().address1("14 Broad St").city("Nashua").state("NH").zip("03064").build();
				}
			}

			/**
			 * The Class AddressEqualsHashCodeTest.
			 */
			public static class AddressEqualsHashCodeTest extends EqualsHashCodeTestCase {

				@Override
				protected Address createInstance() throws Exception {
					return new Address.Builder().address1("2802 South Havana Street").city("Aurora").state("CO").zip("80014").build();
				}

				@Override
				protected Address createNotEqualInstance() throws Exception {
					return new Address.Builder().address1("9839 Carlisle Boulevard NE").city("Albuquerque").state("NM").zip("87110").build();
				}
			}

			/**
			 * The Class AddressSerializabilityTest.
			 */
			public static class AddressSerializabilityTest extends SerializabilityTestCase {

				@Override
				protected Serializable createInstance() throws Exception {
					return new Address.Builder().address1("9839 Carlisle Boulevard NE").city("Albuquerque").state("NM").zip("87110").build();
				}
			}

			public static class AddressMiscTest {

				private Address address;

				/**
				 * Setup.
				 *
				 * @throws Exception the exception
				 */
				@Before
				public void setUp() throws Exception {
					address = new Address.Builder().address1("9839 Carlisle Boulevard NE").city("Albuquerque").state("NM").zip("87110").build();
				}

				/**
				 * Test builder.
				 */
				@Test
				public void testBuilder() {
					assertThat(address.getAddress1(), is("9839 Carlisle Boulevard NE"));
					assertThat(address.getCity(), is("Albuquerque"));
					assertThat(address.getState(), is("NM"));
					assertThat(address.getZip(), is("87110"));
				}

				@Test
				public void testToString() {
					assertThat(address.toString(), is("Address{9839 Carlisle Boulevard NE, Albuquerque, NM, 87110}"));
				}
			}
		}
