Java code can be difficult to test for thread safety when multithreading.

The article at http://www.planetgeek.ch/2009/08/25/how-to-find-a-concurrency-bug-with-java/
describes a method of exposing concurrency bugs that adds a new assertion method `assertConcurrent`, that you pass in a Collection of Runnables that are your arrange\act\assert test on the SUT, the chances of triggering a multithreading code error and failing some assertion are greatly increased:

The assertConcurrent method is:

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





