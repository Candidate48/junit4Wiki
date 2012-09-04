### Rules ###

- Rules allow very flexible addition or redefinition of the behavior
  of each test method in a test class.  Testers can reuse or extend one of the 
  provided Rules below, or write their own.
 
 - For more on this feature, see http://www.threeriversinstitute.org/blog/?p=155

## TemporaryFolder Rule 
- The TemporaryFolder Rule allows creation of files and folders that are guaranteed to be deleted when the test method finishes (whether it passes or fails):

        public static class HasTempFolder {
			@Rule
			public TemporaryFolder folder= new TemporaryFolder();
		
			@Test
			public void testUsingTempFolder() throws IOException {
				File createdFile= folder.newFile("myfile.txt");
				File createdFolder= folder.newFolder("subfolder");
				// ...
			}
		  } 

- `TemporaryFolder#newFolder(String... folderNames)` creates recursively deep temporary folders 
- `TemporaryFolder#newFile()` creates a randomly named new file, and `#newFolder()` creates a randomly named new folder

## ExternalResource Rules 
- ExternalResource is a base class for Rules (like TemporaryFolder)
  that set up an external resource before a test (a file, socket, server,
  database connection, etc.), and guarantee to tear it down afterward:

		public static class UsesExternalResource {
			Server myServer = new Server();
			
			@Rule public ExternalResource resource = new ExternalResource() {
				@Override
				protected void before() throws Throwable {
					myServer.connect();
				};
				
				@Override
				protected void after() {
					myServer.disconnect();
				};
			};
			
			@Test public void testFoo() {
				new Client().run(myServer);
			}
		s}

## ErrorCollector Rule
- The ErrorCollector Rule allows execution of a test to continue
  after the first problem is found (for example, to collect _all_ the 
  incorrect rows in a table, and report them all at once):

		public static class UsesErrorCollectorTwice {
			@Rule
			public ErrorCollector collector= new ErrorCollector();
			
			@Test public void example() {
				collector.addError(new Throwable("first thing went wrong"));
				collector.addError(new Throwable("second thing went wrong"));
			}
		}

## Verifier Rule
- Verifier is a base class for Rules like ErrorCollector, which
  can turn otherwise passing test methods into failing tests if a verification
  check is failed.
	
	   private static String sequence;
	
		public static class UsesVerifier {
			@Rule
			public Verifier collector = new Verifier() {
				@Override
				protected void verify() {
					sequence += "verify ";
				}
			};
	
			@Test
			public void example() {
				sequence += "test ";
			}
		}
	
		@Test
		public void verifierRunsAfterTest() {
			sequence = "";
			assertThat(testResult(UsesVerifier.class), isSuccessful());
			assertEquals("test verify ", sequence);
		}

## TestWatchman Rules
- TestWatchman is a base class for Rules that take note
  of the testing action, without modifying it.
  For example, this class will keep a log of each passing and failing 
  test:
     
		 import static org.junit.Assert.fail;  
		 import org.junit.Rule;
		 import org.junit.Test;
		 import org.junit.rules.TestRule;
		 import org.junit.rules.TestWatcher;
		 import org.junit.runner.Description;
		 import org.junit.runners.model.Statement;
		 
		 public class WatchmanTest {
			 private static String watchedLog;
			 @Rule
			 public TestRule watchman = new TestWatcher() {
				 @Override
				 public Statement apply(Statement base, Description description) {
					 return super.apply(base, description);
				 }
		 
				 @Override
				 protected void succeeded(Description description) {
					 watchedLog += description.getDisplayName() + " " + "success!\n";
				 }
		 
				 @Override
				 protected void failed(Throwable e, Description description) {
					 watchedLog += description.getDisplayName() + " " + e.getClass().getSimpleName() + "\n";
				 }
		 
				 @Override
				 protected void starting(Description description) {
					 super.starting(description);
				 }
		 
				 @Override
				 protected void finished(Description description) {
					 super.finished(description);
				 }
			 };
		 
			 @Test
			 public void fails() {
				 fail();
			 }
		 
			 @Test
			 public void succeeds() {
			 }
		 }

## TestName Rule
- The TestName Rule makes the current test name available inside test methods:

		public class NameRuleTest {
			@Rule public TestName name = new TestName();
			
			@Test public void testA() {
				assertEquals("testA", name.getMethodName());
			}
			
			@Test public void testB() {
				assertEquals("testB", name.getMethodName());
			}
		}

## Timeout Rule
- The Timeout Rule applies the same timeout to all test methods in a class:

		public static class HasGlobalTimeout {
			public static String log;
			
			@Rule public MethodRule globalTimeout = new Timeout(20);
			
			@Test public void testInfiniteLoop1() {
				log+= "ran1";
				for(;;) {}
			}
			
			@Test public void testInfiniteLoop2() {
				log+= "ran2";
				for(;;) {}
			}
		}

## ExpectedException Rules
- The ExpectedException Rule allows in-test specification
  of expected exception types and messages:
    
		public static class HasExpectedException {
			@Rule
			public ExpectedException thrown= ExpectedException.none();
	
			@Test
			public void throwsNothing() {
	
			}
	
			@Test
			public void throwsNullPointerException() {
				thrown.expect(NullPointerException.class);
				throw new NullPointerException();
			}
	
			@Test
			public void throwsNullPointerExceptionWithMessage() {
				thrown.expect(NullPointerException.class);
				thrown.expectMessage("happened?");
				thrown.expectMessage(startsWith("What"));
				throw new NullPointerException("What happened?");
			}
		}
		
### ClassRule ###

The `ClassRule` annotation extends the idea of method-level Rules,
adding static fields that can affect the operation of a whole class.  Any
subclass of `ParentRunner`, including the standard `BlockJUnit4ClassRunner` 
and `Suite` classes, will support `ClassRule`s.

For example, here is a test suite that connects to a server once before
all the test classes run, and disconnects after they are finished:

		@RunWith(Suite.class)
		@SuiteClasses({A.class, B.class, C.class})
		public class UsesExternalResource {
			public static Server myServer= new Server();
		
			@ClassRule
			public static ExternalResource resource= new ExternalResource() {
				@Override
				protected void before() throws Throwable {
					myServer.connect();
				};
		
				@Override
				protected void after() {
					myServer.disconnect();
				};
			};
		}
	

### RuleChain ###

The RuleChain rule allows ordering of TestRules:

    public static class UseRuleChain {
        @Rule
        public TestRule chain= RuleChain
                               .outerRule(new LoggingRule("outer rule")
                               .around(new LoggingRule("middle rule")
                               .around(new LoggingRule("inner rule");
    
        @Test
        public void example() {
            assertTrue(true);
        }
    }

writes the log

    starting outer rule
    starting middle rule
    starting inner rule
    finished inner rule
    finished middle rule
    finished outer rule