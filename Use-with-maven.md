# Maven Dependency
     <dependency>
	    <groupId>junit</groupId>
	    <artifactId>junit-dep</artifactId>
	    <version>4.10</version>
        <scope>test</scope>
     </dependency> 

## Execution
See Maven Surefire plugin http://maven.apache.org/plugins/maven-surefire-plugin/

## Use JUnit and Hamcrest in Maven
In your POM.xml, declare dependency used as JUnit-dep, and also override transitive dependency to Hamcrest-Core, so you can use Hamcrest full library of matchers:

    <dependency>
    	<groupId>org.hamcrest</groupId>
	    <artifactId>hamcrest-core</artifactId>
	    <version>1.3</version>
        <scope>test</scope>
    </dependency>
    <dependency>
	    <groupId>junit</groupId>
	    <artifactId>junit-dep</artifactId>
	    <version>4.10</version>
        <scope>test</scope>
     </dependency>         
    <dependency>
       <groupId>org.hamcrest</groupId>
       <artifactId>hamcrest-library</artifactId>
       <version>1.3</version>
       <scope>test</scope>
    </dependency>
     <dependency>
        <groupId>org.mockito</groupId>
        <artifactId>mockito-core</artifactId>
        <version>1.9.0</version>
        <scope>test</scope>
    </dependency>

## Discover slowest test from Surefire xml output:
The following one-liner described at http://stackoverflow.com/questions/5094410/how-to-list-the-slowest-junit-tests-in-a-multi-module-maven-build

reports on the test times, slowest sorted to the top:

`grep -h "<testcase" `find . -iname "TEST-*.xml"` | sed 's/<testcase time="\(.*\)" classname="\(.*\)" name="\(.*\)".*/\1\t\2.\3/' | sort -rn | head`

