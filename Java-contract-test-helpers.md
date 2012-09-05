Certain code you override or implement is expected to adhere to contracts laid out in the Java SDK.  Examples of these are:
- equals method: http://docs.oracle.com/javase/7/docs/api/java/lang/Object.html#equals(java.lang.Object)
- hashcode method: http://docs.oracle.com/javase/7/docs/api/java/lang/Object.html#hashCode()
- Comparable interface: http://docs.oracle.com/javase/7/docs/api/java/lang/Comparable.html
- Serializable interface: http://docs.oracle.com/javase/7/docs/api/java/io/Serializable.html

A project called junit-addons has test superclasses that enable compliance testing of objects to these java contracts at 
http://junit-addons.sourceforge.net/junitx/extensions/package-frame.html
these test helper classes work without issue, although are designed for pre-generic java, and JUnit 3.x.

An modernized JUnit4 version of these test helpers, with examples, is at https://github.com/chas66/TestHelper

