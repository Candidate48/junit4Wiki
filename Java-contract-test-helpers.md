Certain code you override or implement is expected to adhere to contracts laid out in the Java SDK.  Examples of these are:
- equals method: http://docs.oracle.com/javase/8/docs/api/java/lang/Object.html#equals(java.lang.Object)
- hashcode method: http://docs.oracle.com/javase/8/docs/api/java/lang/Object.html#hashCode()
- Comparable interface: http://docs.oracle.com/javase/8/docs/api/java/lang/Comparable.html
- Serializable interface: http://docs.oracle.com/javase/8/docs/api/java/io/Serializable.html

A project called junit-addons on SourceForge has test superclasses that enable compliance testing of objects to these java contracts
- http://junit-addons.sourceforge.net/junitx/extensions/package-frame.html

Although these test helper classes work without issue, they are designed for pre-generic java, and JUnit 3.x and could be confusing to developers used to JUnit 4.x annotations style of test implementation.

The project [Equals Verifier](https://github.com/jqno/equalsverifier) provides support for testing `equals` and `hashCode`.