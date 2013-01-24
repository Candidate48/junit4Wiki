Java code can be difficult to test for thread safety when multithreading.

The article at http://www.planetgeek.ch/2009/08/25/how-to-find-a-concurrency-bug-with-java/
describes a method of exposing concurrency bugs that adds a new assertion method `assertConcurrent`.  

To use this you pass in a Collection of Runnables that are your arrange\act\assert test on the SUT, they all run at the same time in the `assertConcurrent` method; the chances of triggering a multithreading code error, and thereby failing some assertion are greatly increased:

The `assertConcurrent` method from the article is:

		public static void assertConcurrent(final String message, final List<? extends Runnable> runnables, final int maxTimeoutSeconds) throws InterruptedException {
		  final int numThreads = runnables.size();
		  final List<Throwable> exceptions = Collections.synchronizedList(new ArrayList<Throwable>());
		  final ExecutorService threadPool = Executors.newFixedThreadPool(numThreads);
		  try {
			final CountDownLatch allExecutorThreadsReady = new CountDownLatch(numThreads);
			final CountDownLatch afterInitBlocker = new CountDownLatch(1);
			final CountDownLatch allDone = new CountDownLatch(numThreads);
			for (final Runnable submittedTestRunnable : runnables) {
			  threadPool.submit(new Runnable() {
				public void run() {
				  allExecutorThreadsReady.countDown();
				  try {
					afterInitBlocker.await();
					submittedTestRunnable.run();
				  } catch (final Throwable e) {
					exceptions.add(e);
				  } finally {
					allDone.countDown();
				  }
				}
			  });
			}
			// wait until all threads are ready
			assertTrue("Timeout initializing threads! Perform long lasting initializations before passing runnables to assertConcurrent", allExecutorThreadsReady.await(runnables.size() * 10, TimeUnit.MILLISECONDS));
			// start all test runners
			afterInitBlocker.countDown();
			assertTrue(message +" timeout! More than" + maxTimeoutSeconds + "seconds", allDone.await(maxTimeoutSeconds, TimeUnit.SECONDS));
		  } finally {
			threadPool.shutdownNow();
		  }
		  assertTrue(message + "failed with exception(s)" + exceptions, exceptions.isEmpty());
		}



Another article giving an overview of alternative stragies at [http://tempusfugitlibrary.org/recipes/2012/05/20/testing-concurrent-code/](http://tempusfugitlibrary.org/recipes/2012/05/20/testing-concurrent-code/) might also be useful.

### Java Concurrency Bookshelf

- The Java Memory Model and Thread Specification [JSR-133](http://jcp.org/en/jsr/detail?id=133)
- Threads and Locks, [Java Virtual Machine Specification](http://docs.oracle.com/javase/specs/jvms/se5.0/html/Threads.doc.html)
- The book [Java Concurrency in Practice](http://www.javaconcurrencyinpractice.com) by Brian Goetz ([Amazon UK](http://tinyurl.com/a98yue3)).
- [Double Checked Locking article](http://www.cs.umd.edu/~pugh/java/memoryModel/DoubleCheckedLocking.html) by Doug Lea
- [Doug Lea's homepage](http://g.oswego.edu)