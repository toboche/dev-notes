Notes made when going through https://kotlinlang.org/docs/coroutines-guide.html

Structured concurrency - coroutines are launched only in a CoroutineScope. The coroutine scope is responsible for the
structure and parent-child relationships between different coroutines. Coroutine context stores additional technical
information used to run. There's a parent-child relationship between coroutines created inside of each other (exception:
GlobalScope). The scope can automatically cancel children and it waits for their completion.

* `runBlocking()`- create a coroutine scope, block current thread.
* `coroutineScope`- create a couroutine scope and suspend (without blocking the current thread).
* `launch{}`- build coroutine, return a job
* `job.join()`- suspend until coroutine is finished
* `job.cancel()`- cancel the job
* `job.cancelAndJoin()`- ...
* `CoroutineScope.isActive`- to check if a coroutine has been cancelled. Has to be done "manually" in "
  custom
* `yield()` - can be used to check if the coroutine is interrupted
  coroutines". Because of that cancellation is said to be cooperative.
* Use `finally` to close resources, wrap in `withContext(NonCancellable)` if the release of resources is blocking
* `withTimeout` - schedule with timeout, throw `CancellationException` when interrupted
* `withTimeoutOrNull()` - schedule with timeout, don't throw but return `null` when interrupted
* `async` - similar to launch, but returns a `Deferred`
* `Deferred` - non blocking promise, inherits from `Job`, can be `await()`'ed. Can also be called
  with `CoroutineStart.LAZY` and then be `start()`'ed on your own.
* `GlobalScope.async{}` - non-blocking, rather unsafe (no structured concurrency) way of declaring async function.
  Better
  approach - use `coroutineScope{}`.
* Coroutines are sequential by default. To make them concurrent, you can start many `async{}`s and then `awaitAll()` for
  them. You can also change the dispatcher at the same time.
* `withContext` - calls the specified code with specified context and suspends until it's done. This is a shorter form
  of `launch(context){...}.join()`
* Randezvous channel - channel without a buffer. Both `send()` and `receive()` suspend, until a new element is received
  or
  sent.
* Unlimited channel - `send()` never suspends. Buffer is unlimited. OOMs can happen
* Buffered channel - buffer size is set. Both operations can suspend
* Conflated channel - a new element sent always overrides the old one.
* `runTest{}` - allows running tests with a controlled clock. `currentTime` can be used to get the "fake" time.
* `Dispatchers.Unconfined` - starts on the outer scope's until first suspension. Then it resumes on another thread.
* `newSingleThreadContext(name: String)` - create a new dispatcher with a new, dedicated thread
* `couroutineContext[Job]` - used to get the current job within a coroutine
* `async(CoroutineName("test"))` - set a debug name of the coroutine
* `launch(Dispatchers.Default + CoroutineName("test"))` - this is how one can combine different context elements
* `ThreadLocal.asContextElement` can be used to keep the value of a given `ThreadLocal` and restore it every time the
  coroutine switches the context
* `flow{}` - used to create `Flow<>`'s. Functions using it are not suspend. Values emitted by `emit()` and collected
  by `collect()`. Flows are cold. Alternatively, one can use `.asFlow()` extension and `flowOf()`. You can
  use `map`, `filter`, etc. on flows but they can use suspending functions. These operators are cold too.
* `transform()` - general operator that can `emit()` as many times as it wants
* size limiting operators (e.g. `take`) cause throwing an exception
* terminal operators (e.g. `toList`, `toSet`, `first`, `single`, `reduce`, `fold`, `collect`) are suspending
* Collections of flow are performed sequentially, a value is emitted, then processed and collected. Only after that
  another value is emitted.
* Context preservation - collection is performed in the context of the calling coroutine. This is the default behaviour
  of `flow{}` too. This means `emit()` cannot be called in other context by calling `withContext()`.
* `flowOn()` - the right way to change the context of a `flow{}`. It creates a new coroutine to execute the upstream.
* `buffer()` - run flow emitting code concurrently
* `conflate()` - skip intermediate values, whenever a newer one is available. It drops emitted values when the collector
  is too slow to process them.
* `collectLatest()` - Cancel a slow collector and restart it every time a new value is emitted. There are
  more `xxxLatest()` operators.
* `zip()` - zip two flows (item #1 with item #1, item #2 with item #2, etc.)
* `combine()` - transform the latest values of each of the flows, every time a value is emitted in any of the streams
* `flatMapConcat()`, `flattenConcat` - used to join two flows in a sequential matter (the first one has to finish before
  the second is collected)
* `flatMapMerge`, `flattenMerge` - join two flows, but this time _concurrently_ (ASAP). Additional
  parameter `concurrency` can be used to set the limit of max concurrent flows to be collected. The transformation
  operation is called sequentially.
* `flatMapLatest` - only transform the latest values, dropping the transformation for the previous ones
* Flows collectors throw when the emitters throw. Try/catch can be used because of that.
* 