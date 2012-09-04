# Assumptions

Ideally, the developer writing a test has control of all of the forces that might cause a test to fail. If this isn't immediately possible, making dependencies explicit can often improve a design. 
For example, if a test fails when run in a different locale than the developer intended, it can be fixed by explicitly passing a locale to the domain code.

However, sometimes this is not desirable or possible. 
It's good to be able to run a test against the code as it is currently written, implicit assumptions and all, or to write a test that exposes a known bug. For these situations, JUnit now includes the ability to express "assumptions":

    import static org.junit.Assume.*
    @Test public void filenameIncludesUsername() {
        assumeThat(File.separatorChar, is('/'));
        assertThat(new User("optimus").configFileName(), is("configfiles/optimus.cfg"));
    }

    @Test public void correctBehaviorWhenFilenameIsNull() {
       assumeTrue(bugFixed("13356"));  // bugFixed is not included in JUnit
       assertThat(parse(null), is(new NullDocument()));
    }

A failed assumption will lead to the test being marked as passing, regardless of what the code below the assumption may assert. In the future, this may change, and a failed assumption may lead to the test being ignored: however, third-party runners do not currently allow this option.

We have included assumeTrue for convenience, but thanks to the inclusion of Hamcrest, we do not need to create assumeEquals, assumeSame, and other analogues to the assert* methods. All of those functionalities are subsumed in assumeThat, with the appropriate matcher.

A failing assumption in a `@Before` or `@BeforeClass` method will have the same effect as a failing assumption in each `@Test` method of the class.