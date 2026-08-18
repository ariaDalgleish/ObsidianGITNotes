Task 5.1 and Task 5.2

Teaching:
Main Thread
Start
Syncronized
## Task 5.1 Multiple Threads
#### Requirements:
Find Counter.java from Task05_1 package. It can print all odd numbers from 1 to 10.
- Modify `Counter.java` to use a `Thread` instance to print odd numbers 1–10
- Extend it to use **two threads** — one printing odd numbers, one printing even numbers (1–10)
- Extend further so the two threads print **one odd and one even number per second** (paired output using timing control, e.g. `sleep()`)

#### Working:

Counter (default)
``` java
public class Counter {

    int num;

    public static void main(String[] args) {
        Counter count = new Counter(1);
        count.printNum();
    }

    public Counter(int i) {
        this.num = i;
    }

    public void printNum() {
        for (int j = this.num; j <= 10; j += 2) {
            System.out.print(j + " ");
        }
    }
}
```

Make `Counter` implement `Runnable` (or extend `Thread`) and wrap it in a `Thread` object:
``` java
package Task05_1;

public class Counter implements Runnable {

    int num;

    public static void main(String[] args) {
        Counter count = new Counter(1);
        Thread t = new Thread(count);
        t.start();
    }

    public Counter(int i) {
        this.num = i;
    }

    @Override
    public void run() {
        for (int j = this.num; j <= 10; j += 2) {
            System.out.print(j + " ");
        }
    }
}
```
This mirrors the "Create Threads (Solution 1)" pattern from the lecture — `run()` replaces `printNum()`, and `main()` now creates a `Thread` and calls `.start()` instead of calling the method directly.

Next step:
Add a starting-number parameter so you can spin up two `Counter` instances, one starting at 1 (odds) and one at 2 (evens):
``` java
package Task05_1;

public class Counter implements Runnable {

    int num;

    public static void main(String[] args) {
        Counter oddCounter = new Counter(1);
        Counter evenCounter = new Counter(2);

        Thread oddThread = new Thread(oddCounter);
        Thread evenThread = new Thread(evenCounter);

        oddThread.start();
        evenThread.start();
    }

    public Counter(int i) {
        this.num = i;
    }

    @Override
    public void run() {
        for (int j = this.num; j <= 10; j += 2) {
            System.out.print(j + " ");
        }
    }
}
```
Note the output order between the two threads won't be guaranteed — that's expected at this stage (same idea as the Ping Pong example where thread scheduling isn't deterministic).

Next step:
This is where you bring in `Thread.sleep()`, like the Ping Pong Sleep example. The key design decision: each thread should print **one number**, then sleep, then print the next — and both threads use the _same_ delay so they roughly pair up:
``` java
package Task05_1;

public class Counter implements Runnable {

    int num;

    public static void main(String[] args) {
        Counter oddCounter = new Counter(1);
        Counter evenCounter = new Counter(2);

        Thread oddThread = new Thread(oddCounter);
        Thread evenThread = new Thread(evenCounter);

        oddThread.start();
        evenThread.start();
    }

    public Counter(int i) {
        this.num = i;
    }

    @Override
    public void run() {
        for (int j = this.num; j <= 10; j += 2) {
            System.out.print(j + " ");
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                System.out.println("Interrupted");
            }
        }
    }
}
```
This gets you close, but plain `sleep()` on two independent threads only _approximately_ pairs the numbers — there's no strict guarantee thread A's number 1 prints before thread B's number 2 finishes its own cycle. If your tutorial expects strict pairing (one odd immediately followed by its even partner, every second, in lockstep), you'd need to go further than what's shown in the lecture and add coordination — e.g. a shared flag with `wait()`/`notify()` (the Car factory pattern) so each thread waits for its turn before printing.

Worth checking: does your tutorial spec want "roughly one pair per second" (independent sleeping threads, good enough) or "strictly alternating, synchronized pairs" (needs `wait()`/`notify()`)? That changes which version you should submit.
## Task 5.2 Thread Communications
#### Requirements 
Modify the program, make it be able to output the same figure by using inter-thread
communications. You need to have two threads. One is for printing stars and the
other one for printing spaces. (You may need to create more classes in this package)

- Given program outputs a pyramid of stars (1, 3, 5, 7… stars per line, right-aligned)
- Task: reproduce the same output using **two threads** communicating with each other — one thread printing stars, the other printing spaces — using inter-thread communication (`wait()`/`notify()`)
- May require creating additional helper classes

#### Working
| Car factory                                     | Star figure                                           |
| ----------------------------------------------- | ----------------------------------------------------- |
| `carAvailable` boolean flag                     | `spacesTurn` boolean flag                             |
| `make()` waits if a car is already available    | `printSpaces()` waits if it's not the spaces' turn    |
| `get()` waits if no car is available            | `printStars()` waits if it's not the stars' turn      |
| `notify()` after changing flag                  | `notify()` after changing flag                        |
| Producer/Consumer alternate on one shared `Car` | Space/Star threads alternate on one shared  `Printer` |



Star.java (unmodified)
```java
package Task05_2;

public class Star {

    public static void main(String[] args) {
        int max = 9;
        Star aStar = new Star();
        System.out.println("Figure:");
        aStar.printStar(max);

    }

    private void printStar(int rowNumber) {

        for (int i = 1; i <= rowNumber; i++) {

            //Print spaces
            for (int j = 0; j < (9 - i); j++) {
                System.out.print(" ");
            }

            //Print stars
            for (int j = 0; j < (2 * i - 1); j++) {
                System.out.print("*");
            }
            System.out.println();
        }
    }
}
```

Solution:
Figure.java

``` java
package Task05_2;

public class Figure {
    // define two states
    public static final boolean STAR_PRINTED = true;
    public static final boolean SPACE_PRINTED = false;

    // space should print first each row, so flag starts as STAR_PRINTED
    boolean flag = STAR_PRINTED;

    // synchronized: blocks other threads while this method is running
    synchronized void printSpace(int n) {
        if (flag != STAR_PRINTED) {
            try {
                wait();
            } catch (InterruptedException e) {
                System.out.println("InterruptedException caught");
            }
        }
        for (int i = 0; i < (9 - n); i++) {
            System.out.print(" ");
        }
        flag = SPACE_PRINTED;
        // wakes up the thread waiting to print stars
        notify();
    }

    synchronized void printStar(int n) {
        if (flag != SPACE_PRINTED) {
            try {
                wait();
            } catch (InterruptedException e) {
                System.out.println("InterruptedException caught");
            }
        }
        for (int i = 0; i < (2 * n - 1); i++) {
            System.out.print("*");
        }
        System.out.println();
        flag = STAR_PRINTED;
        // wakes up the thread waiting to print spaces
        notify();
    }
}
```

FigurePrint.java
```java 
package Task05_2;

public class FigurePrint {

    public static void main(String[] args) {

        Figure fig = new Figure();
        Space ap = new Space(fig);
        Star at = new Star(fig);

        Thread spaceThread = new Thread(ap, "Space");
        spaceThread.start();

        Thread starThread = new Thread(at, "Star");
        starThread.start();
    }
}
```
Space.java
package Task05_2;

``` java
public class Space implements Runnable {

    private Figure fig;
    private int max;

    public Space(Figure fig) {
        this.fig = fig;
        this.max = 9;
    }

    @Override
    public void run() {
        for (int i = 1; i <= max; i++) {
            fig.printSpace(i);
        }
    }
}
```
Star.java
``` java
package Task05_2;

public class Star implements Runnable {

    private Figure fig;
    private int max;

    public Star(Figure fig) {
        this.fig = fig;
        this.max = 9;
    }

    @Override
    public void run() {
        for (int i = 1; i <= max; i++) {
            fig.printStar(i);
        }
    }
}
```

syncronized int printSpace
synchronized void printStar
booleans to check star or space printed