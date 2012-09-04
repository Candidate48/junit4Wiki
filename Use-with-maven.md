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
