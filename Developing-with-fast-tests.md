### How to execute JUnit with fast tests ###

If you are the JUnit developer, you can launch our unit tests faster and thus save your private time a bit.
This means launch the build process with Maven profile "fast-tests".

In command line you can execute the Maven build with concurrent tests:
```mvn test -P fast-tests```