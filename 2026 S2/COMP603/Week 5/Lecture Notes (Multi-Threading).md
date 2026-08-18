
#### Process vs Thread

- **Process**: self-contained execution environment with its own private resources — address space, memory space, data access (e.g., opening a Word document)
- **Thread**: shares the process's resources (memory, open files) — requires fewer resources than creating a new process
- A single process can run multiple threads concurrently (e.g., a word processor running auto-save and spell-check alongside the main editing task)
- On a single-processor system, threads take turns executing (interleaved); on a multi-processor system, threads can run truly in parallel

#### Single-Threaded vs Multi-Threaded

- Single-threaded program: `main()` executes sequentially, begin → body → end
- Multi-threaded program: main thread spawns multiple threads (A, B, C) that run concurrently
- **Advantages**: better resource utilisation, improved responsiveness, ability to perform multiple tasks simultaneously

#### Creating Threads in Java

- Core class: `java.lang.Thread`
- Key methods: `start()`, `setPriority(int)`, `join()`, `sleep(long)`, `yield()`, `interrupt()`
- **Two ways to create a thread:**
    1. **Implement `Runnable`** — create a task class implementing `Runnable` (with a `run()` method), then wrap it: `Thread t = new Thread(task); t.start();`
    2. **Extend `Thread`** — create a class that extends `Thread` and overrides `run()`, then call `.start()` directly on an instance
- `Thread` itself implements `Runnable`

#### Running & Naming Threads

- Call `start()` to begin a new thread (never call `run()` directly if you want concurrency)
- `Thread.currentThread()` — returns the currently executing thread object
- `isAlive()` — checks if a thread has started and not yet terminated
- `setName()` — changes a thread's name
- The **main thread** starts automatically when a program runs, with default name `"main"` and priority 5

#### Thread States (Lifecycle)

- **Newly Created** → **Start Thread** → **Runnable** (eligible to run, waiting to be scheduled) → **Running** → either back to Runnable, to **Blocked/Waiting/Sleeping** (not eligible to run but still alive — e.g. waiting on I/O, sleeping), or to **Dead** (terminated, cannot be revived)

#### Thread Priority

- Every thread has a priority from **1 (lowest)** to **10 (highest)**
- Constants: `Thread.MAX_PRIORITY` (10), `Thread.NORM_PRIORITY` (5, default), `Thread.MIN_PRIORITY` (1)
- Set with `aThread.setPriority(int)`
- Higher priority = higher **chance** of being selected by the scheduler — **not a guarantee**

#### yield() and sleep()

- `yield()`: pauses the current thread temporarily, allowing other threads a chance to execute
- `sleep(long millis)`: blocks the current thread for a specified time; throws `InterruptedException` if interrupted while sleeping
- Example (Ping Pong Sleep): two threads printing "ping"/"PONG" with different delay times interleave based on their sleep durations

#### interrupt()

- `interrupt()`: does **not** stop a thread — it just sets the thread's "interrupted" status to `true`, so the program can then decide what action to take
- `isInterrupted()`: checks interrupted status **without** clearing it
- `interrupted()`: checks interrupted status and **clears** it afterward
- These distinctions matter for how repeated checks behave in a loop

#### join()

- `aThread.join(long millis)`: makes the calling thread wait for `aThread` to finish (or until timeout); `0` = wait forever until it dies
- Throws `InterruptedException`
- Must be called **before** the thread is scheduled/dispatched by the processor
- Example: calling `ping.join()` before `pong.start()` forces all of "ping" to print before "pong" starts

#### Synchronization

- Needed when two or more threads share the same resource — race conditions can cause unexpected/interleaved output
- **Synchronized method**: add the `synchronized` keyword to a method declaration
- When one thread is executing a synchronized method on an object, all other threads calling synchronized methods on that **same object** block until the first thread finishes
- Example: unsynchronized `CallMe.call()` produces garbled output (`[ping[PONG]]`); adding `synchronized` fixes it so each call completes in full before the next begins

#### join() vs synchronized — key difference

- `synchronized` locks access to a **shared resource/method** — any thread calling that specific method is blocked, but each thread is free to do other work afterward
- `join()` blocks the **calling thread entirely** until the joined thread completes — it doesn't just protect one method call, it holds up everything downstream (e.g., if "ping" calls a second method after `call()`, `join()` still waits for the whole thread to finish, not just the shared method)

#### Lock Objects (ReentrantLock)

- `ReentrantLock` (from `java.util.concurrent.locks`) offers explicit locking of critical sections to one thread at a time
- Pattern:

java

```java
  myLock.lock();
  try {
      // critical section
  } finally {
      myLock.unlock();
  }
```

- **Important**: always unlock in a `finally` block — otherwise other threads could be blocked forever if an exception is thrown inside the critical section

#### Inter-Thread Communication

- **Polling problem**: repeatedly checking a condition in a loop wastes CPU cycles
- Java's solution: `wait()`, `notify()`, `notifyAll()` — but these can **only** be called from within a `synchronized` method
- **Rules:**
    - `wait()`: calling thread gives up the lock and sleeps until another thread calls `notify()`
    - `notify()`: wakes up the first thread waiting on that object
    - `notifyAll()`: wakes up all threads waiting on that object
- **Example — Car factory (producer/consumer)**: a car can only be made if the previous one has been sold, and can only be sold if one is available
    - Without `wait()/notify()`, the producer just keeps overproducing regardless of consumption
    - Fix: use a `carAvailable` boolean flag; `get()` waits if no car is available, `make()` waits if a car is already available; each calls `notify()` after changing the flag to wake the other thread