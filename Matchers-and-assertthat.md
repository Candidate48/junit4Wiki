# assertThat

Joe Walnes built a new assertion mechanism on top of what was then JMock 1. The method name was assertThat, and the syntax looked like this:

```java
assertThat(x, is(3));
assertThat(x, is(not(4)));
assertThat(responseString, either(containsString("color")).or(containsString("colour")));
assertThat(myList, hasItem("3"));
```

More generally:

```java
assertThat([value], [matcher statement]);
```

Advantages of this assertion syntax include:

More readable and typeable: this syntax allows you to think in terms of subject, verb, object (assert "x is 3") rather than `assertEquals`, which uses verb, object, subject (assert "equals 3 x")

Combinations: any matcher statement s can be negated (`not(s)`), combined (`either(s).or(t)`), mapped to a collection (`each(s)`), or used in custom combinations (`afterFiveSeconds(s)`)

Readable failure messages. Compare:

```java
assertTrue(responseString.contains("color") || responseString.contains("colour"));
// ==> failure message: 
// java.lang.AssertionError:


assertThat(responseString, anyOf(containsString("color"), containsString("colour")));
// ==> failure message:
// java.lang.AssertionError: 
// Expected: (a string containing "color" or a string containing "colour")
//      got: "Please choose a font"
```

Custom Matchers. By implementing the Matcher interface yourself, you can get all of the above benefits for your own custom assertions.

For a more thorough description of these points, see Joe Walnes's original post.

We have decided to include this API directly in JUnit. It's an extensible and readable syntax, and it enables new features, like assumptions and theories.

Some notes:

The old assert methods are never, ever, going away. Developers may continue using the old assertEquals, assertTrue, and so on.
The second parameter of an assertThat statement is a Matcher. We include the Matchers we want as static imports, like this:

```java
import static org.hamcrest.CoreMatchers.is;
```

or:

```java
import static org.hamcrest.CoreMatchers.*;
```

Manually importing Matcher methods can be frustrating. Eclipse 3.3 includes the ability to define "Favorite" classes to import static methods from, which makes it easier (Search for "Favorites" in the Preferences dialog). We expect that support for static imports will improve in all Java IDEs in the future.

To allow compatibility with a wide variety of possible matchers, we have decided to include the classes from hamcrest-core, from the Hamcrest project. This is the first time that third-party classes have been included in JUnit.

JUnit currently ships with a few matchers, defined in `org.hamcrest.CoreMatchers` and `org.junit.matchers.JUnitMatchers`.
 
To use many, many more, consider downloading the full hamcrest package:
* Hamcrest page http://code.google.com/p/hamcrest/wiki/Tutorial
* Hamcrest Java on GitHub: https://github.com/hamcrest/JavaHamcrest

JUnit contains special support for comparing string and array values, giving specific information on how they differ. This is not yet available using the assertThat syntax, but we hope to bring the two assert methods into closer alignment in future releases.

# JUnit Matchers
JUnit includes useful matchers for use with the assertThat method, but they are not currently included in the basic CoreMatchers class from hamcrest.
- Javadoc JUnitMatchers [http://junit-team.github.com/junit/javadoc/latest/org/junit/matchers/JUnitMatchers.html](http://junit-team.github.com/junit/javadoc/latest/org/junit/matchers/JUnitMatchers.html)

# Hamcrest CoreMatchers
Useful Hamcrest CoreMatchers are included in the JUnit distribution
- JavaDoc Hamcrest CoreMatchers [http://junit-team.github.com/junit/javadoc/latest/org/hamcrest/core/package-summary.html](http://junit-team.github.com/junit/javadoc/latest/org/hamcrest/core/package-summary.html)

# Thirdparty Matchers
Other, potentially Matchers out there include
- [Excel spreadsheet matchers](https://github.com/tobyweston/simple-excel)
- [JSON matchers](https://github.com/hertzsprung/hamcrest-json)
- [XML/XPath matchers](https://code.google.com/p/xml-matchers/)