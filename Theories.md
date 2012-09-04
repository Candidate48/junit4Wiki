Theories

More flexible and expressive assertions, combined with the ability to state assumptions clearly, lead to a new kind of statement of intent, which we call a "Theory". A test captures the intended behavior in one particular scenario. A theory captures some aspect of the intended behavior in possibly infinite numbers of potential scenarios. For example:

    @RunWith(Theories.class)
    public class UserTest {
      @DataPoint public static String GOOD_USERNAME = "optimus";
      @DataPoint public static String USERNAME_WITH_SLASH = "optimus/prime";
    
      @Theory public void filenameIncludesUsername(String username) {
           assumeThat(username, not(containsString("/")));
           assertThat(new User(username).configFileName(), containsString(username));
      }
    }

This makes it clear that the user's filename should be included in the config file name, only if it doesn't contain a slash. Another test or theory might define what happens when a username does contain a slash.

UserTest will attempt to run filenameIncludesUsername on every compatible DataPoint defined in the class. If any of the assumptions fail, the data point is silently ignored. If all of the assumptions pass, but an assertion fails, the test fails.

The support for Theories has been absorbed from the Popper project, and more complete documentation can be found there.

Defining general statements in this way can jog the developer's memory about other potential data points and tests, also allows automated tools to search for new, unexpected data points that expose bugs.