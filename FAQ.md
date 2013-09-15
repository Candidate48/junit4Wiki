_JUnit is a simple, open source framework to write and run repeatable tests. It is an instance of the xUnit architecture for unit testing frameworks._

Edited by [Mike Clark](mailto:mike@clarkware.com) (http://clarkware.com)

Last modified on February 20, 2006

###Table of Contents

1. FAQ Info
 1. Who is responsible for this FAQ?
 2. How can I contribute to this FAQ?
 3. Where do I get the latest version of this FAQ?

2. Overview
 1. What is JUnit?
 2. Where is the JUnit home page?
 3. Where are the JUnit mailing lists and forums?
 4. Where is the JUnit documentation?
 5. Where can I find articles on JUnit?
 6. What's the latest news on JUnit?
 7. How is JUnit licensed?
 8. What awards has JUnit won?

3. Getting Started
 1. Where do I download JUnit?
 2. How do I install JUnit?
 3. How do I uninstall JUnit?
 4. How do I ask questions?
 5. How do I submit bugs, patches, or feature requests?

4. Writing Tests
 1. How do I write and run a simple test?
 2. How do I use a test fixture?
 3. How do I test a method that doesn't return anything?
 4. Under what conditions should I test get() and set() methods?
 5. Under what conditions should I not test get() and set() methods?
 6. How do I write a test that passes when an expected exception is thrown?
 7. How do I write a test that fails when an unexpected exception is thrown?
 8. How do I test protected methods?
 9. How do I test private methods?
 10. Why does JUnit only report the first failure in a single test?
 11. In Java 1.4, 'assert' is a keyword. Won't this conflict with JUnit's assert() method?
 12. How do I test things that must be run in a J2EE container (e.g. servlets, EJBs)?
 13. Do I need to write a test class for every class I need to test?
 14. Is there a basic template I can use to create a test?
 15. How do I write a test for an abstract class?
 16. When are tests garbage collected?

5. Organizing Tests
 1. Where should I put my test files?
 2. How can I run setUp() and tearDown() code once for all of my tests?

6. Running Tests
 1. What CLASSPATH settings are needed to run JUnit?
 2. Why do I get a NoClassDefFoundError when trying to test JUnit or run the samples?
 3. How do I run JUnit from my command window?
 4. How do I run JUnit using Ant?
 5. How do I use Ant to create HTML test reports?
 6. How do I pass command-line arguments to a test execution?
 7. Why do I get a LinkageError when using XML interfaces in my test class?
 8. Why do I get the warning "AssertionFailedError: No tests found in XXX" when I run my test?
 9. Why do I see "Unknown Source" in the stack trace of a test failure, rather than the source file's line number?
 10. How do I organize all test classes in a TestSuite automatically and not use or manage a TestSuite explicitly?

7. Best Practices
 1. When should tests be written?
 2. Do I have to write a test for everything?
 3. How simple is 'too simple to break'?
 4. How often should I run my tests?
 5. What do I do when a defect is reported?
 6. Why not just use System.out.println()?
 7. Why not just use a debugger?

8. Miscellaneous
 1. How do I integrate JUnit with my IDE?
 2. How do I launch a debugger when a test fails?
 3. Where can I find unit testing frameworks similar to JUnit for other languages?

###FAQ Info
1. Who is responsible for this FAQ?

    The current version of this FAQ is maintained by Mike Clark.

    Most of the wisdom contained in this FAQ comes from the collective insights and hard-won experiences of the many good folks who participate on the JUnit mailing list and the JUnit community at large.

    If you see your genius represented anywhere in this FAQ without due credit to you, please send me an email and I'll make things right.

2. How can I contribute to this FAQ?

    Your contributions to this FAQ are greatly appreciated! The JUnit community thanks you in advance.

    To contribute to this FAQ, simply write a JUnit-related question and answer, then send the unformatted text to Mike Clark. Corrections to this FAQ are always appreciated, as well.

    No reasonable contribution will be denied. Your name will always appear along with any contribution you make.

3. Where do I get the latest version of this FAQ?

    The master copy of this FAQ is available at http://junit.sourceforge.net/doc/faq/faq.htm.

    The JUnit distribution also includes this FAQ in the doc directory.

###Overview

1. What is JUnit?

    JUnit is a simple, open source framework to write and run repeatable tests. It is an instance of the xUnit architecture for unit testing frameworks. JUnit features include:
        Assertions for testing expected results
        Test fixtures for sharing common test data
        Test runners for running tests

    JUnit was originally written by Erich Gamma and Kent Beck.

2. Where is the JUnit home page?

    The official JUnit home page is http://junit.org.

3. Where are the JUnit mailing lists and forums?

    There are 3 mailing lists dedicated to everything JUnit:
        JUnit user list. (Search it for answers to frequently asked questions not included here.)
        JUnit announcements
        JUnit developer list

4. Where is the JUnit documentation?

    The following documents are included in the JUnit distribution in the doc directory:
        JUnit Test Infected: Programmers Love Writing Tests
        JUnit Cookbook
        JUnit - A Cook's Tour
        JUnit FAQ

5. Where can I find articles on JUnit?

    The JUnit home page maintains a list of JUnit articles.

6. What's the latest news on JUnit?

    The JUnit home page publishes the latest JUnit news.

7. How is JUnit licensed?

    JUnit is Open Source Software, released under the Eclipse Public License Version 1.0 and hosted on SourceForge.

8. What awards has JUnit won?

        2002 JavaWorld Editors' Choice Awards (ECA)

        Best Java Performance Monitoring/Testing Tool

        2001 JavaWorld Editors' Choice Awards (ECA)

        Best Java Performance Monitoring/Testing Tool

###Getting Started

1. Where do I download JUnit?

    The latest version of JUnit is available on SourceForge.

2. How do I install JUnit?

        First, download the latest version of JUnit, referred to below as junit.zip.

        Then install JUnit on your platform of choice:

        Windows

        To install JUnit on Windows, follow these steps:

            Unzip the junit.zip distribution file to a directory referred to as %JUNIT_HOME%.
            Add JUnit to the classpath:

            set CLASSPATH=%CLASSPATH%;%JUNIT_HOME%\junit.jar

        Unix (bash)

        To install JUnit on Unix, follow these steps:

            Unzip the junit.zip distribution file to a directory referred to as $JUNIT_HOME.

            Add JUnit to the classpath:

            export CLASSPATH=$CLASSPATH:$JUNIT_HOME/junit.jar

        (Optional) Unzip the $JUNIT_HOME/src.jar file.

        Test the installation by running the sample tests distributed with JUnit. Note that the sample tests are located in the installation directory directly, not the junit.jar file. Therefore, make sure that the JUnit installation directory is on your CLASSPATH. Then simply type:

            java org.junit.runner.JUnitCore org.junit.tests.AllTests 

        All the tests should pass with an "OK" message.

        If the tests don't pass, verify that junit.jar is in the CLASSPATH.

        Finally, read the documentation.

3. How do I uninstall JUnit?

        Delete the directory structure where you unzipped the JUnit distribution.

        Remove junit.jar from the CLASSPATH.

    JUnit does not modify the registry so simply removing all the files will fully uninstall it.

4. How do I ask questions?

    Questions that are not answered in the FAQ or in the documentation should be posted to the jGuru discussion forum or the JUnit user mailing list.

    Please stick to technical issues on the discussion forum and mailing lists. Keep in mind that these are public, so do not include any confidental information in your questions!

    You should also read "How to ask questions the smart way" by Eric Raymond before participating in the discussion forum and mailing lists.

    NOTE:
    Please do NOT submit bugs, patches, or feature requests to the discussion forum or mailing lists.
    Refer instead to "How do I submit bugs, patches, or feature requests?".

5. How do I submit bugs, patches, or feature requests?

    JUnit celebrates programmers testing their own software. In this spirit, bugs, patches, and feature requests that include JUnit tests have a better chance of being addressed than those without.

    JUnit is hosted on SourceForge. Please use the tools provided by SourceForge for your submissions.

###Writing Tests

1. How do I write and run a simple test?

        Create a class:


        	      
          package junitfaq;
        	      
          import org.junit.*;
          import static org.junit.Assert.*;

          import java.util.*;
          
          public class SimpleTest {
        	  

        Write a test method (annotated with @Test) that asserts expected results on the object under test:



            @Test
            public void testEmptyCollection() {
                Collection collection = new ArrayList();
                assertTrue(collection.isEmpty());
            }
        	  

        If you are running your JUnit 4 tests with a JUnit 3.x runner, write a suite() method that uses the JUnit4TestAdapter class to create a suite containing all of your test methods:



            public static junit.framework.Test suite() {
                return new junit.framework.JUnit4TestAdapter(SimpleTest.class);
            }
        	  

        Although writing a main() method to run the test is much less important with the advent of IDE runners, it's still possible:



            public static void main(String args[]) {
              org.junit.runner.JUnitCore.main("junitfaq.SimpleTest");
            }
          }
        	  

        Run the test:

            To run the test from the console, type:

                java org.junit.runner.JUnitCore junitfaq.SimpleTest 

            To run the test with the test runner used in main(), type:

                java junitfaq.SimpleTest 

        The passing test results in the following textual output:


            		.
            Time: 0

            OK (1 tests)
            	    

2. How do I use a test fixture?

    (Submitted by: Jeff Nielsen)

    A test fixture is useful if you have two or more tests for a common set of objects. Using a test fixture avoids duplicating the code necessary to initialize (and cleanup) the common objects.

    Tests can use the objects (variables) in a test fixture, with each test invoking different methods on objects in the fixture and asserting different expected results. Each test runs in its own test fixture to isolate tests from the changes made by other tests. That is, tests don't share the state of objects in the test fixture. Because the tests are isolated, they can be run in any order.

    To create a test fixture, declare instance variables for the common objects. Initialize these objects in a public void method annotated with @Before. The JUnit framework automatically invokes any @Before methods before each test is run.

    The following example shows a test fixture with a common Collection object.


        package junitfaq;

        import org.junit.*;
        import static org.junit.Assert.*;
        import java.util.*;

        public class SimpleTest {

            private Collection<Object> collection;

            @Before
            public void setUp() {
                collection = new ArrayList<Object>();
            }

            @Test
            public void testEmptyCollection() {
                assertTrue(collection.isEmpty());
            }


            @Test
            public void testOneItemCollection() {
                collection.add("itemA");
                assertEquals(1, collection.size());
            }
        }
          

    Given this test, the methods might execute in the following order:

        setUp()
        testEmptyCollection()
        setUp()
        testOneItemCollection()

    The ordering of test-method invocations is not guaranteed, so testOneItemCollection() might be executed before testEmptyCollection(). But it doesn't matter, because each method gets its own instance of the collection.

    Although JUnit provides a new instance of the fixture objects for each test method, if you allocate any external resources in a @Before method, you should release them after the test runs by annotating a method with @After. The JUnit framework automatically invokes any @After methods after each test is run. For example:


        package junitfaq;

        import org.junit.*;
        import static org.junit.Assert.*;
        import java.io.*;

        public class OutputTest {

            private File output;

            @Before
            public void createOutputFile() {
                output = new File(...);
            }

            @After
            public void deleteOutputFile() {
                output.delete();
            }

            @Test
            public void testSomethingWithFile() {
                ...
            }
        }
          

    With this test, the methods will execute in the following order:


        createOutputFile()
        testSomethingWithFile()
        deleteOutputFile()
                

3. How do I test a method that doesn't return anything?

    (Submitted by: Dave Astels)

    Often if a method doesn't return a value, it will have some side effect. Actually, if it doesn't return a value AND doesn't have a side effect, it isn't doing anything.

    There may be a way to verify that the side effect actually occurred as expected. For example, consider the add() method in the Collection classes. There are ways of verifying that the side effect happened (i.e. the object was added). You can check the size and assert that it is what is expected:



        @Test
        public void testCollectionAdd() {
            Collection collection = new ArrayList();
            assertEquals(0, collection.size());
            collection.add("itemA");
            assertEquals(1, collection.size());
            collection.add("itemB");
            assertEquals(2, collection.size());
        }
          

    Another approach is to make use of MockObjects.

    A related issue is to design for testing. For example, if you have a method that is meant to output to a file, don't pass in a filename, or even a FileWriter. Instead, pass in a Writer. That way you can pass in a StringWriter to capture the output for testing purposes. Then you can add a method (e.g. writeToFileNamed(String filename)) to encapsulate the FileWriter creation.

4. Under what conditions should I test get() and set() methods?

    Unit tests are intended to alleviate fear that something might break. If you think a get() or set() method could reasonably break, or has in fact contributed to a defect, then by all means write a test.

    In short, test until you're confident. What you choose to test is subjective, based on your experiences and confidence level. Remember to be practical and maximize your testing investment.

    Refer also to "How simple is 'too simple to break'?".

5. Under what conditions should I not test get() and set() methods?

    (Submitted by: J. B. Rainsberger)

    Most of the time, get/set methods just can't break, and if they can't break, then why test them? While it is usually better to test more, there is a definite curve of diminishing returns on test effort versus "code coverage". Remember the maxim: "Test until fear turns to boredom."

    Assume that the getX() method only does "return x;" and that the setX() method only does "this.x = x;". If you write this test:

        @Test
        public void testGetSetX() {
            setX(23);
            assertEquals(23, getX());
        }
              

    then you are testing the equivalent of the following:

        @Test
        public void testGetSetX() {
            x = 23;
            assertEquals(23, x);
        }

    or, if you prefer,

        @Test
        public void testGetSetX() {
            assertEquals(23, 23);
        }

    At this point, you are testing the Java compiler, or possibly the interpreter, and not your component or application. There is generally no need for you to do Java's testing for them.

    If you are concerned about whether a property has already been set at the point you wish to call getX(), then you want to test the constructor, and not the getX() method. This kind of test is especially useful if you have multiple constructors:

        @Test
        public void testCreate() {
            assertEquals(23, new MyClass(23).getX());
        }
              

6. How do I write a test that passes when an expected exception is thrown?

    Add the optional expected attribute to the @Test annotation. The following is an example test that passes when the expected IndexOutOfBoundsException is raised:



        @Test(expected=IndexOutOfBoundsException.class)
        public void testIndexOutOfBoundsException() {
            ArrayList emptyList = new ArrayList();
    	Object o = emptyList.get(0);
        }
          

7. How do I write a test that fails when an unexpected exception is thrown?

    Declare the exception in the throws clause of the test method and don't catch the exception within the test method. Uncaught exceptions will cause the test to fail with an error.

    The following is an example test that fails when the IndexOutOfBoundsException is raised:



        @Test
        public void testIndexOutOfBoundsExceptionNotRaised() 
            throws IndexOutOfBoundsException {
        
            ArrayList emptyList = new ArrayList();
            Object o = emptyList.get(0);
        }
          

8. How do I test protected methods?

    Place your tests in the same package as the classes under test.

    Refer to "Where should I put my test files?" for examples of how to organize tests for protected method access.

9. How do I test private methods?

    Testing private methods may be an indication that those methods should be moved into another class to promote reusability.

    But if you must...

    If you are using JDK 1.3 or higher, you can use reflection to subvert the access control mechanism with the aid of the PrivilegedAccessor. For details on how to use it, read this article.

10. Why does JUnit only report the first failure in a single test?

    (Submitted by: J. B. Rainsberger)

    Reporting multiple failures in a single test is generally a sign that the test does too much, compared to what a unit test ought to do. Usually this means either that the test is really a functional/acceptance/customer test or, if it is a unit test, then it is too big a unit test.

    JUnit is designed to work best with a number of small tests. It executes each test within a separate instance of the test class. It reports failure on each test. Shared setup code is most natural when sharing between tests. This is a design decision that permeates JUnit, and when you decide to report multiple failures per test, you begin to fight against JUnit. This is not recommended.

    Long tests are a design smell and indicate the likelihood of a design problem. Kent Beck is fond of saying in this case that "there is an opportunity to learn something about your design." We would like to see a pattern language develop around these problems, but it has not yet been written down.

    Finally, note that a single test with multiple assertions is isomorphic to a test case with multiple tests:

    One test method, three assertions:


        public class MyTestCase {
            @Test
            public void testSomething() {
                // Set up for the test, manipulating local variables
                assertTrue(condition1);
                assertTrue(condition2);
                assertTrue(condition3);
            }
        }
              

    Three test methods, one assertion each:


        public class MyTestCase {
            // Local variables become instance variables

            @Before
            public void setUp() {
                // Set up for the test, manipulating instance variables
            }
            
            @Test
            public void testCondition1() {
                assertTrue(condition1);
            }

            @Test
            public void testCondition2() {
                assertTrue(condition2);
            }

            @Test
            public void testCondition3() {
                assertTrue(condition3);
            }
        }
              

    The resulting tests use JUnit's natural execution and reporting mechanism and, failure in one test does not affect the execution of the other tests. You generally want exactly one test to fail for any given bug, if you can manage it.

    In Java 1.4, assert is a keyword. Won't this conflict with JUnit's assert() method?

    JUnit 3.7 deprecated assert() and replaced it with assertTrue(), which works exactly the same way.

    JUnit 4 is compatible with the assert keyword. If you run with the -ea JVM switch, assertions that fail will be reported by JUnit.

11. How do I test things that must be run in a J2EE container (e.g. servlets, EJBs)?

    Refactoring J2EE components to delegate functionality to other objects that don't have to be run in a J2EE container will improve the design and testability of the software.

    Cactus is an open source JUnit extension that can be used to test J2EE components in their natural environment.

12. Do I need to write a test class for every class I need to test?

    (Submitted by: J. B. Rainsberger)

    No. It is a convention to start with one test class per class under test, but it is not necessary.

    Test classes only provide a way to organize tests, nothing more. Generally you will start with one test class per class under test, but then you may find that a small group of tests belong together with their own common test fixture.[1] In this case, you may move those tests to a new test class. This is a simple object-oriented refactoring: separating responsibilities of an object that does too much.

    Another point to consider is that the TestSuite is the smallest execution unit in JUnit: you cannot execute anything smaller than a TestSuite at one time without changing source code. In this case, you probably do not want to put tests in the same test class unless they somehow "belong together". If you have two groups of tests that you think you'd like to execute separately from one another, it is wise to place them in separate test classes.

    [1] A test fixture is a common set of test data and collaborating objects shared by many tests. Generally they are implemented as instance variables in the test class.

    Is there a basic template I can use to create a test?

    (Submitted by: Eric Armstrong)

    The following templates are a good starting point. Copy/paste and edit these templates to suit your coding style.

    SampleTest is a basic test template:


        import org.junit.*;
        import static org.junit.Assert.*;

        public class SampleTest {

            private java.util.List emptyList;

            /**
             * Sets up the test fixture. 
             * (Called before every test case method.)
             */
            @Before
            public void setUp() {
                emptyList = new java.util.ArrayList();
            }

            /**
             * Tears down the test fixture. 
             * (Called after every test case method.)
             */
            @After
            public void tearDown() {
                emptyList = null;
            }
            
            @Test
            public void testSomeBehavior() {
                assertEquals("Empty list should have 0 elements", 0, emptyList.size());
            }

            @Test(expected=IndexOutOfBoundsException.class)
            public void testForException() {
                Object o = emptyList.get(0);
            }
        }
              

    How do I write a test for an abstract class?

    Refer to http://c2.com/cgi/wiki?AbstractTestCases.

    When are tests garbage collected?

    (Submitted by: Timothy Wall and Kent Beck)

    By design, the tree of Test instances is built in one pass, then the tests are executed in a second pass. The test runner holds strong references to all Test instances for the duration of the test execution. This means that for a very long test run with many Test instances, none of the tests may be garbage collected until the end of the entire test run.

    Therefore, if you allocate external or limited resources in a test, you are responsible for freeing those resources. Explicitly setting an object to null in the tearDown() method, for example, allows it to be garbage collected before the end of the entire test run.

###Organizing Tests

1. Where should I put my test files?

    You can place your tests in the same package and directory as the classes under test.

    For example:

        src
           com
              xyz
                 SomeClass.java
                 SomeClassTest.java	 
              

    While adequate for small projects, many developers feel that this approach clutters the source directory, and makes it hard to package up client deliverables without also including unwanted test code, or writing unnecessarily complex packaging tasks.

    An arguably better way is to place the tests in a separate parallel directory structure with package alignment.

    For example:

        src
           com
              xyz
                 SomeClass.java
        test
           com
              xyz
                 SomeClassTest.java	 
              

    These approaches allow the tests to access to all the public and package visible methods of the classes under test.

    Some developers have argued in favor of putting the tests in a sub-package of the classes under test (e.g. com.xyz.test). The author of this FAQ sees no clear advantage to adopting this approach and believes that said developers also put their curly braces on the wrong line. :-)

2. How can I run setUp() and tearDown() code once for all of my tests?

    The desire to do this is usually a symptom of excessive coupling in your design. If two or more tests must share the same test fixture state, then the tests may be trying to tell you that the classes under test have some undesirable dependencies.

    Refactoring the design to further decouple the classes under test and eliminate code duplication is usually a better investment than setting up a shared test fixture.

    But if you must...

    You can add a @BeforeClass annotation to a method to be run before all the tests in a class, and a @AfterClass annotation to a method to be run after all the tests in a class. Here's an example:



        package junitfaq;

        import org.junit.*;
        import static org.junit.Assert.*;
        import java.util.*;
        
        public class SimpleTest {
        
            private Collection collection;
    	
            @BeforeClass
            public static void oneTimeSetUp() {
                // one-time initialization code        
            }

            @AfterClass
            public static void oneTimeTearDown() {
                // one-time cleanup code
            }

            @Before
            public void setUp() {
                collection = new ArrayList();
            }
    	
            @After
            public void tearDown() {
                collection.clear();
            }

            @Test
            public void testEmptyCollection() {
                assertTrue(collection.isEmpty());
            }
    	
            @Test
            public void testOneItemCollection() {
                collection.add("itemA");
                assertEquals(1, collection.size());
            }
        }
          

    Given this test, the methods will execute in the following order:


        oneTimeSetUp()
        setUp()
        testEmptyCollection()
        tearDown()
        setUp()
        testOneItemCollection()
        tearDown()
        oneTimeTearDown()
        	

###Running Tests

1. What CLASSPATH settings are needed to run JUnit?

    (Submitted by: Eric Armstrong)

    To run your JUnit tests, you'll need the following elemements in your CLASSPATH:
        JUnit class files
        Your class files, including your JUnit test classes
        Libraries your class files depend on

    If attempting to run your tests results in a NoClassDefFoundError, then something is missing from your CLASSPATH.

    Windows Example:

    set CLASSPATH=%JUNIT_HOME%\junit.jar;c:\myproject\classes;c:\myproject\lib\something.jar

    Unix (bash) Example:

    export CLASSPATH=$JUNIT_HOME/junit.jar:/myproject/classes:/myproject/lib/something.jar

2. Why do I get a NoClassDefFoundError when trying to test JUnit or run the samples?

    (Submitted by: J.B. Rainsberger and Jason Rogers)

    Most likely your CLASSPATH doesn't include the JUnit installation directory.

    Refer to "What CLASSPATH settings are needed to run JUnit?" for more guidance.

    Also consider running WhichJunit to print the absolute location of the JUnit class files required to run and test JUnit and its samples.

    If the CLASSPATH seems mysterious, read this!

3. How do I run JUnit from my command window?

    (Submitted by: Eric Armstrong)

        Set your CLASSPATH

        Invoke the runner:

        java org.junit.runner.JUnitCore <test class name>

4. How do I run JUnit using Ant?

    (Submitted by: Eric Armstrong)

        Define any necessary Ant properties:


        <property name="src" value="./src" />
        <property name="lib" value="./lib" />
        <property name="classes" value="./classes" />
        <property name="test.class.name" value="com.xyz.MyTestSuite" />
        	  

        Set up the CLASSPATH to be used by JUnit:


        <path id="test.classpath">
          <pathelement location="${classes}" />
          <pathelement location="/path/to/junit.jar" />
          <fileset dir="${lib}">
            <include name="**/*.jar"/>
          </fileset>
        </path>
        	  

        Define the Ant task for running JUnit:


        <target name="test">
          <junit fork="yes" haltonfailure="yes">
            <test name="${test.class.name}" />
            <formatter type="plain" usefile="false" />
            <classpath refid="test.classpath" />
          </junit>
        </target>
        	  

        Run the test:
        ant test

    Refer to the JUnit Ant Task for more information.

5. How do I use Ant to create HTML test reports?

    (Submitted by: Eric Armstrong and Steffen Gemkow)

        Ensure that Ant's optional.jar file is either in your CLASSPATH or exists in your $ANT_HOME/lib directory.

        Add an ANT property for the directory containing the HTML reports:
        <property name="test.reports" value="./reports" />

        Define the Ant task for running JUnit and generating reports:


        <target name="test-html">
          <junit fork="yes" printsummary="no" haltonfailure="no">
            <batchtest fork="yes" todir="${test.reports}" >
              <fileset dir="${classes}">
                <include name="**/*Test.class" />
              </fileset>
            </batchtest>
            <formatter type="xml" />
            <classpath refid="test.classpath" />
          </junit>

          <junitreport todir="${test.reports}">
            <fileset dir="${test.reports}">
              <include name="TEST-*.xml" />
            </fileset>
            <report todir="${test.reports}" />
          </junitreport>
        </target>
        	  

        Run the test:
        ant test-html

    Refer to the JUnit Ant Task for more information.

6. How do I pass command-line arguments to a test execution?

    Use the -D JVM command-line options, as in:

        -DparameterName=parameterValue 

    If the number of parameters on the command line gets unweildy, pass in the location of a property file that defines a set of parameters. Alternatively, the JUnit-addons package contains the XMLPropertyManager and PropertyManager classes that allow you to define a property file (or XML file) containing test parameters.

7. Why do I get a LinkageError when using XML interfaces in my test?

    (Submitted by: Scott Stirling)

    The workaround as of JUnit 3.7 is to add org.w3c.dom.* and org.xml.sax.* to your excluded.properties.

    It's just a matter of time before this fix becomes incorporated into the released version of JUnit's excluded.properties, since JAXP is a standard part of JDK 1.4. It will be just like excluding org.omg.*. By the way, if you download the JUnit source from its Sourceforge CVS, you will find that these patterns have already been added to the default excluded.properties and so has a pattern for JINI. In fact, here is the current version in CVS, which demonstrates how to add exclusions to the list too:

        #
        # The list of excluded package paths for the TestCaseClassLoader
        #
        excluded.0=sun.*
        excluded.1=com.sun.*
        excluded.2=org.omg.*
        excluded.3=javax.*
        excluded.4=sunw.*
        excluded.5=java.*
        excluded.6=org.w3c.dom.*
        excluded.7=org.xml.sax.*
        excluded.8=net.jini.*
              

    This is the most common case where the default excluded.properties list needs modification. The cause of the LinkageError is related to using JAXP in your test cases. By JAXP I mean the whole set of javax.xml.* classes and the supporting org.w3c.dom.* and org.xml.sax.* classes.

    As stated above, the JUnit GUI TestRunners' classloader relies on the excluded.properties for classes it should delegate to the system classloader. JAXP is an unusual case because it is a standard Java extension library dependent on classes whose package names (org.w3c.dom.* and org.xml.sax.*) do not begin with a standard Java or Sun prefix. This is similar to the relationship between javax.rmi.* and the org.omg.* classes, which have been excluded by default in JUnit'ss excluded.properties for a while.

    What can happen, and frequently does when using the JUnit Swing or AWT UI with test cases that reference, use or depend on JAXP classes, such as Log4J, Apache SOAP, Axis, Cocoon, etc., is that the JUnit class loader (properly) delegates javax.xml.* classes it "sees" to the system loader. But then the system loader, in the process of initializing and loading that JAXP class, links and loads up a bunch of org.w3c.dom/org.xml.sax classes. When it does so, the JUnit custom classloader is not involved at all because the system classloader never delegates "down" or checks with custom classloaders to see if a class is already loaded. At any point after this, if the JUnit loader is asked to load an org.w3c.dom/org.xml.sax class that it's never seen before, it will try to load it because the class' name doesn't match any of the patterns in the default exclude list. That's when a LinkageError occurs. This is really a flaw in the JUnit classloader design, but there is the workaround given above.

    Java 2 JVMs keep classes (remember, classes and objects, though related, are different entities to the JVM - I'm talking about classes here, not object instances) in namespaces, identifying them by their fully qualified classname plus the instance of their defining (not initiating) loader. The JVM will attempt to assign all unloaded classes referenced by an already defined and loaded class to that class's defining loader. The JVM's classresolver routine (implemented as a C function in the JVM source code) keeps track of all these class loading events and "sees" if another classloader (such as the JUnit custom loader) attempts to define a class that has already been defined by the system loader. According to the rules of Java 2 loader constraints, in case a class has already been defined by the system loader, any attempts to load a class should first be delegated to the system loader. A "proper" way for JUnit to handle this feature would be to load classes from a repository other than the CLASSPATH that the system classloader knows nothing about. And then the JUnit custom classloader could follow the standard Java 2 delegation model, which is to always delegate class loading to the system loader, and only attempt to load if that fails. Since they both load from the CLASSPATH in the current model, if the JUnit loader delegated like it's supposed to, it would never get to load any classes since the system loader would always find them.

    You could try to hack around this in the JUnit source by catching the LinkageError in TestCaseClassLoader's loadClass() method and then making a recovery call to findSystemClass() -- thereby delegating to the system loader after the violation has been caught. But this hack only works some of the time, because now you can have the reverse problem where the JUnit loader will load a host of org.w3c.dom/org.xml.sax classes, and then the system loader violates the loader contraints at some point when it tries to do exactly what I described above with JAXP because it doesn't ever delegate to its logical child (the JUnit loader). Inevitably, if your test cases use many JAXP and related XML classes, one or the other classloader will end up violating the constraints whatever you do.

8. Why do I get the warning "AssertionFailedError: No tests found in XXX" when I run my test?

    Make sure you have more or more method annotated with @Test.

    For example:

        @Test
        public void testSomething() {
        }
              

9. Why do I see "Unknown Source" in the stack trace of a test failure, rather than the source file's line number?

    The debug option for the Java compiler must be enabled in order to see source file and line number information in a stack trace.

    When invoking the Java compiler from the command line, use the -g option to generate all debugging info.

    When invoking the Java compiler from an Ant task, use the debug="on" attribute. For example:

        <javac srcdir="${src}" destdir="${build}" debug="on" /> 

    When using older JVMs pre-Hotspot (JDK 1.1 and most/all 1.2), run JUnit with the -DJAVA_COMPILER=none JMV command line argument to prevent runtime JIT compilation from obscuring line number info.

    Compiling the test source with debug enabled will show the line where the assertion failed. Compiling the non-test source with debug enabled will show the line where an exception was raised in the class under test.

10. How do I organize all test classes in a TestSuite automatically and not use or manage a TestSuite explicitly?

    (Submitted by: Bill de hora)

    There are a number of ways to do this:

        In Ant, use the junit task and the batchtest element:


        <junit printsummary="yes" haltonfailure="yes">
          ...
          <batchtest fork="yes">
            <fileset dir="${src.dir}">
               <include name="**/*Test.java" />
               <include name="**/Test*.java" />
            </fileset>
          </batchtest>
        </junit> 
        	  

        Idiomatic naming patterns for unit tests are Test*.java and *Test.java. Documentation and examples are at http://ant.apache.org/manual/OptionalTasks/junit.html.

        Use the DirectorySuiteBuilder and ArchiveSuiteBuilder (for jar/zip files) classes provided by JUnit-addons project:

            DirectorySuiteBuilder builder = new DirectorySuiteBuilder();
            builder.setSuffix("Test");
            Test suite = builer.suite("/home/project/myproject/tests"); 
            	  

        Documentation and examples are at http://junit-addons.sourceforge.net.

        Write your own custom suite builder.

        Have your test classes implement an interface and write a treewalker to load each class in a directory, inspect the class, and add any classes that implement the interface to a TestSuite.

        You might only want to do this if you are very uncomfortable with using a naming convention for test classes. Aside from being slow for larger suites, ultimately it's arguable whether it's more effort to follow a naming convention that have test classes implement an interface!

        An example of this approach is at http://www.javaworld.com/javaworld/jw-12-2000/jw-1221-junit_p.html.

###Best Practices

1. When should tests be written?

    Tests should be written before the code. Test-first programming is practiced by only writing new code when an automated test is failing.

    Good tests tell you how to best design the system for its intended use. They effectively communicate in an executable format how to use the software. They also prevent tendencies to over-build the system based on speculation. When all the tests pass, you know you're done!

    Whenever a customer test fails or a bug is reported, first write the necessary unit test(s) to expose the bug(s), then fix them. This makes it almost impossible for that particular bug to resurface later.

    Test-driven development is a lot more fun than writing tests after the code seems to be working. Give it a try!

2. Do I have to write a test for everything?

    No, just test everything that could reasonably break.

    Be practical and maximize your testing investment. Remember that investments in testing are equal investments in design. If defects aren't being reported and your design responds well to change, then you're probably testing enough. If you're spending a lot of time fixing defects and your design is difficult to grow, you should write more tests.

    If something is difficult to test, it's usually an opportunity for a design improvement. Look to improve the design so that it's easier to test, and by doing so a better design will usually emerge.

3. How simple is 'too simple to break'?

    (Submitted by: J. B. Rainsberger)

    The general philosophy is this: if it can't break on its own, it's too simple to break.

    First example is the getX() method. Suppose the getX() method only answers the value of an instance variable. In that case, getX() cannot break unless either the compiler or the interpreter is also broken. For that reason, don't test getX(); there is no benefit. The same is true of the setX() method, although if your setX() method does any parameter validation or has any side effects, you likely need to test it.

    Next example: suppose you have written a method that does nothing but forward parameters into a method called on another object. That method is too simple to break.

        public void myMethod(final int a, final String b) {
            myCollaborator.anotherMethod(a, b);
        }
              

    myMethod cannot possibly break because it does nothing: it forwards its input to another object and that's all.

    The only precondition for this method is "myCollaborator != null", but that is generally the responsibility of the constructor, and not of myMethod. If you are concerned, add a test to verify that myCollaborator is always set to something non-null by every constructor.

    The only way myMethod could break would be if myCollaborator.anotherMethod() were broken. In that case, test myCollaborator, and not the current class.

    It is true that adding tests for even these simple methods guards against the possibility that someone refactors and makes the methods "not-so-simple" anymore. In that case, though, the refactorer needs to be aware that the method is now complex enough to break, and should write tests for it -- and preferably before the refactoring.

    Another example: suppose you have a JSP and, like a good programmer, you have removed all business logic from it. All it does is provide a layout for a number of JavaBeans and never does anything that could change the value of any object. That JSP is too simple to break, and since JSPs are notoriously annoying to test, you should strive to make all your JSPs too simple to break.

    Here's the way testing goes:

        becomeTimidAndTestEverything
        while writingTheSameThingOverAndOverAgain
            becomeMoreAggressive
            writeFewerTests
            writeTestsForMoreInterestingCases
            if getBurnedByStupidDefect
                feelStupid
                becomeTimidAndTestEverything
            end
        end
              

    The loop, as you can see, never terminates.

4. How often should I run my tests?

    Run all your unit tests as often as possible, ideally every time the code is changed. Make sure all your unit tests always run at 100%. Frequent testing gives you confidence that your changes didn't break anything and generally lowers the stress of programming in the dark.

    For larger systems, you may just run specific test suites that are relevant to the code you're working on.

    Run all your acceptance, integration, stress, and unit tests at least once per day (or night).

    If you're using Eclipse, be sure to check out David Saff's continuous testing plug-in.

5. What do I do when a defect is reported?

    Test-driven development generally lowers the defect density of software. But we're all fallible, so sometimes a defect will slip through. When this happens, write a failing test that exposes the defect. When the test passes, you know the defect is fixed!

    Don't forget to use this as a learning opportunity. Perhaps the defect could have been prevented by being more aggressive about testing everything that could reasonably break.

6. Why not just use System.out.println()?

    Inserting debug statements into code is a low-tech method for debugging it. It usually requires that output be scanned manually every time the program is run to ensure that the code is doing what's expected.

    It generally takes less time in the long run to codify expectations in the form of an automated JUnit test that retains its value over time. If it's difficult to write a test to assert expectations, the tests may be telling you that shorter and more cohesive methods would improve your design.

7. Why not just use a debugger?

    Debuggers are commonly used to step through code and inspect that the variables along the way contain the expected values. But stepping through a program in a debugger is a manual process that requires tedious visual inspections. In essence, the debugging session is nothing more than a manual check of expected vs. actual results. Moreover, every time the program changes we must manually step back through the program in the debugger to ensure that nothing broke.

    It generally takes less time to codify expectations in the form of an automated JUnit test that retains its value over time. If it's difficult to write a test to assert expected values, the tests may be telling you that shorter and more cohesive methods would improve your design.

###Miscellaneous

1. How do I integrate JUnit with my IDE?

    The JUnit home page maintains a list of IDE integration instructions.

2. How do I launch a debugger when a test fails?

    Start the TestRunner under the debugger and configure the debugger so that it catches the junit.framework.AssertionFailedError.

    How you configure this depends on the debugger you prefer to use. Most Java debuggers provide support to stop the program when a specific exception is raised.

    Notice that this will only launch the debugger when an expected failure occurs.

3. Where can I find unit testing frameworks similar to JUnit for other languages?

    XProgramming.com maintains a complete list of available xUnit testing frameworks.

