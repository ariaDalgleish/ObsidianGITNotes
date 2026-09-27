## **Desktop Pet with daily calendar.**

Sources:
https://www.baeldung.com/reading-file-in-java
https://www.baeldung.com/java-hashmap
CORE JAVA Volume 1: Fundamentals , Fourteenth Edition. Cay S. Horstmann

Pet States:
1. Sleep
	1. Pet is sleeping, the application is running in background to save power and memory it is limited to very small run time.
	2. After a certain amount of time and the pet has not been interacted with, the application will return to sleep mode until woken.
2. Idle
	1. By mouse clicking on the virtual pet, the pet "wakes up" with an alerted animation and the application is now fully interactable.
	2. If no calendar has been imported, prompt for user to add URL. Otherwise calendar displays the date and the events of that day.
		1.  Have way for player to import calendar link that's easy to use and understand.
		2. Code implements calendar web url
	3. Once calendar is imported, Pet gives two options to switch date display on daily calendar - previous goes back a day, next goes forward a day. 
		1. GUI version: 
		   Two buttons "pop" out (left arrow key button and right arrow key button), these buttons control the calendar pages. The buttons are interactable through mouse click input on the button, or by pressing the keyboard arrow keys. 
		2. Left arrow button flips the page over to show the previous day
		3. Right arrow button flips the page over to show the next day.
	4. Interacting with the pet changes state to active.
3. Active
	1. Selecting an option the pet acts accordingly, with GUI a simple animation of flipping the calendar page.
	2. Handles logic for updating the calendar.

conditional in "wake" flow, something like: check if `CalendarSource` is set → if null, print "No calendar imported. Enter a URL:" → else fetch and display today's events.

**How to flip pages back and forth?**
- Main interaction - mouseclick
- Mouse click then activates virtual pet from idle (sleep)
- Once active different interaction buttons are unlocked:
- Pop up buttons of keyboard inputs that also use mouse click interaction.
 **Calendar setup**
- Have way for player to import calendar link that's easy to use and understand.
- Code implements web url.
**Sleep saves computer performance since it'll run in the background.**
- Restricted inputs to make project achievable.
- Implements both mouse and keyboard inputs.
- Sync calendar to google or cloud calendar or any URL 

![[canvas_desktop-calendar-pet-260722_0117 1.png]]


Calendar format:
Square "widget" display date and daily scheduled events.
Date: SUN , 06 Sep
	3 letter format. Day of the week title, Number of day, month title. 

Underneath in order from earliest event to latest event. Events layout vertical stacking.
Event format: Time | Title ... Location (under in smaller font)
10:00 | Church
1 Valley Rd 
	Time is 24hr display, if title is too long fade out end with "...", location is underneath in smaller writing. 
	Each event is wrapped in a rectangle with filled background color of the event's color. 

Stick to java.time package and friends.

I don't want the calendar to be interactable just to display information from an already made calendar such as date and scheduled events for the day. Only interactable functions will be to change the day to previous or next day, and a settings to import calendar URL.


PLAN:
CUI Assignment. Text menu to interact with pet - print "Your pet wakes up". No event handling, sprite animations etc. 
State machine (idle/acive/sleeping) driven by menu choices, a CalendarEvent/Calendar Source structure, reading/writing a text file, and a loop that prints menus and reads input.


Monday




Tuesday

Wednesday

Thursday

Friday
Write up documentation and record short video.


CUI Menu:

On run:

| State    | CUI                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| On run   | *Checks for calendar source*<br>*No calendar found* = "Import calendar URL to proceed..."<br>*Calendar found move to sleeping pet state + dialogue*                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| Sleeping | ""zzz..." Pet is sleeping shh, do you want to wake up pet? (Type anything)"<br>*User types something and enters -> Awake state*                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| Awake    | *start idle timer (timer stops when state is exited, e.g. pet state changes to active timer stops then starts again when awake state is called)*<br>*If  timer reaches n return to sleep state*<br><br>""Mmmrm" Your pet wakes up!"<br>*If daily calendar is already displayed skip to drop menu*<br>*Display daily calendar* <br>"Date"<br>"Event"<br>*If no scheduled events found ->* "Nothing to do today!"<br><br>*Drop menu:*<br>"Type "Next" to view next day's schedule"<br>"Type "Back" to view previous day's schedule"<br>"Type "Reset" to view the current day."<br><br>*If user types unrecognized command*<br>""Hmmm?" Your pet tilts head in confusion"<br>*If user types command change state to active* |
| Active   | The is how the pet executes actions.<br>Although Active state is short lived it's still necessary step. It executes the pet's actions and dialogues and creates a reset point for the idle timer.<br><br>*Next command* "Pet flips calendar's page foward!"<br>*Back command* "Pet flips calendar's page back!"<br>*Reset command* "Pet flips calendar's page foward!"<br>*Display according daily calendar* <br>"Date"<br>"Event"<br>*If no scheduled events found ->* "Nothing to do today!"<br>*Return to idle state*<br>                                                                                                                                                                                             |
Although Active state is short lived it's still necessary step. It executes the pet's actions and dialogues and creates a reset point for the idle timer. 

Classes design log:

### `Main`
#### Purpose


#### Fields


#### Key Methods


#### OOP concepts demonstrated


#### Relationships to other classes




---

### `Pet`
#### Purpose


#### Fields


#### Key Methods


#### OOP concepts demonstrated


#### Relationships to other classes

---

### `PetState`
``` java
public enum PetState { SLEEPING, AWAKE, ACTIVE }
```
#### Purpose
Three possible states the pet can be in at any moment using Enum.
#### Fields
No fields as they are constants themselves (`SLEEPING`, `AWAKE`, `ACTIVE`).

#### OOP concepts demonstrated
`PetState` **abstracts** away "what stage is the pet at" into three clear, named possibilities, instead of the rest of the code juggling raw strings or magic numbers that are easy to typo or misuse.
#### Relationships to other classes
The enum states are held in `Pet`'s field handling the behavior of each value.

---

### `CalendarEvent`
final means no other class can extend CalendarEvent, it is a standalone concept. 
before anything is assignend check for null. location is different because it is allowed to be missing, becoming an empty string. 

`compareTo` must return negative/zero/positive depending on whether `this` comes before/equal/after `other`. Reusing `LocalTime`'s own logic.
`toString` override lets me control what appears in the format.
#### Purpose
Data-holding class to represent a single event on the specific date.
"Church at 10:00 at 1 Valley Rd"
#### Fields
``` java
private final LocalDate date;
private final LocalTime time;
private final String title;
private final String location;
```
Private and final fields. Once a `CalendarEvent` is created it's values can never be reassigned. The object is **immutable**.
#### Key Methods

**Constructor** takes all values at once and validates them, if something is wrong an `IllegalArgumentException` is thrown. For other classes to read an events data I've used **Getters**. Then `compareTo()` implements the `Comparable<CalendarEvent>` interface so a list of events can be sorted automatically, earliest first. This is what lets `LocalFileCalendarSource` display a day's events chronologically without writing custom sorting logic.
`toString()` overrides Java's default object-to-string conversion so printing a `CalendarEvent` produces a readable line like `10:00 | Church` with the location on the next line.
#### OOP concepts demonstrated
Using private fields, no setters, validated constructor is demonstrating **Encapsulation** as the object protects it's internal state.

#### Relationships to other classes
Class is created and stored by `LocalFileCalendarSource`. The data is displayed by `Pet` class printing each returned `CalendarEvent`. 

### `CalendarSource`
#### Purpose
This is the interface that lets `Pet` ask for events without knowing or caring what type of file etc.

#### Key Methods
``` java
List<CalendarEvent> getEventsFor(LocalDate date); boolean isConfigured();
```
Neither method has a body. It says *what* must be doable, not *how* 
Boolean to check if it's ready to use yet, if the calendar is imported.
#### OOP concepts demonstrated
Abstraction for anything that can supply calendar events.
The Pet class only ever talks to this interface, never to a concrete implementation directly - this is what lets you add a web/URL-based source later without changing Pet at all (Open/Closed + Dependency Inversion principles).

#### Relationships to other classes

`Pet` holds a `CalendarSource` field. `LocalFileCalendarSource implements CalendarSource`, providing the real logic. `CalendarSource` itself references `CalendarEvent` (as the return type) but nothing else.

---

### `LocalFileCalendarSource`
Reading file of calendar
Map/List are private fields. Nothing outside this class can reach in and modify `eventsByDate` `getEventsFor(date)` is the way out which hands back a read-only view for one specific day. Protecting internal data structure from being messed with by other classes.

`loadFromFile()` **core reading logic**
Checks the file is actually there before trying to open. If not stop.

`try (BufferedReader reader = new BufferedReader(new FileReader(filePath.toFile())))`  
From Lecture about I/O, Text File Input. To open a text file for input connect a text file to a stream for reading. `BufferedReader` object uses `FileReader` to open text file, `FileReader` "connects" `BufferedReader` to the text file.

However I'm using a **try-with-resources** block. It guarantees the file gets closed automatically even if something goes wrong while reading, without you writing a manual `finally { reader.close(); }`
Why use  **try-with-resources** ?
- **Safer** - resources are always closed, even if an exception occurs.
- **Cleaner** - no need to write `close()` calls.
- **Shorter code** - less boilerplate, easier to read.

`while ((line = reader.readLine()) != null)` loop reads one line at a time until the file ends.

`import java.nio.file.Files;`
`import java.nio.file.Path;`

Each line gets handed to `parseAndStore(line)` wrapped in its own try/catch so a fail fail isn't a big deal. 
#### Purpose


#### Fields


#### Key Methods


#### OOP concepts demonstrated


#### Relationships to other classes


---


Bug: I forgot to make `CalendarSource` an interface and instead declared as a class.

`DateTimeFormatter` Javadoc.
Used as guide for references.
Format is default ISO `uuuu-MMM-dd`

Design is currently local meaning there is no time zone only just the date, not time of day. How to make sure it's correct time region? 
Make sure its english?

Possible features:
Choose language and time zone.

Perhaps after importing calendar prompt will show asking if the time zone and language "  " is correct, and if they'd like to change.

UPDATE

OnRunCheck is skipped. Url prompt never shows. I believe this is because the enter key is answering to the name prompt and skipping this skip or methods are called at same time? 
Actually no. It's because it goes straight to sleep state after running if on a boolean which isn't set up because Calendarsource needs to be set up properly.
Or it's because the Calendar.txt file is already found?
Bug - user can just press enter insteading of typing to enter awake state.



Bug - Idle, when pet falls asleep from inactivity it doesn't print to output until user types a command and sometimes never times out? Is this is I'm alt tabbed out of netbeans it doesn't keep going.


calendar.txt :
2026-09-10,07:50,Work
2026-09-10,18:00,COMP712,WS313 AUT
2026-09-11,14:00,COMP719 Tutorial,WF402 AUT City Campus
2026-09-13,10:00,Church,1 Valley Rd

bug time out. `scanner.nextLine()` is a **blocking** call.
once your program reaches that line, execution completely stops and waits, potentially forever, until you type something and hit Enter

**The fix — poll for input instead of blocking on it**, using `System.in.available()` to check whether there's actually a line ready to read _before_ committing to `nextLine()`:

Timeout function: readLineWithTimeout()
I had a bug where it would never timeout because I would use scanner.nextLink() blocking the timer from running.

By using `System.in.available()` to check whether there's actually a line ready to read _before_ committing to `nextLine()`:
If nothing's been typed yet, so instead of freezing on a full read, it checks `idleTimedOut()` right then, and if not timed out yet, sleeps for just 200ms and loops around to check again. Short enough that the timeout feels responsive, long enough that the loop isn't hammering the CPU.
It is not the most precise as it reports *bytes* waiting, but it is a stand approach for a CUI.


Script:
I started with the idea of developing a virtual desktop pet, but I thought it'd make for a much better project if it had a useful function.
A virtual pet lets user interact to maybe give inputs, click buttons, play animations. I would want my virtual pet to display reminders for myself.
I'm always using my calendar to keep track of my tight schedules of what's happening and where I need to be at what time. 


ToDO:
- A custom checked exception class (e.g. `CalendarImportException`) instead of catching generic `IOException` everywhere — this also strengthens your "robust error handling" score separately.
- Splitting console output/input handling out of `Pet` into something like a `ConsoleView` or `MenuRenderer` class — `Pet` currently mixes state logic _and_ all the printing/reading, which is worth separating for a cleaner Single Responsibility story anyway.
- persist the pet's name, language, and last-used date to a settings file
- Settings to select language


ConsoleView class.
Pet no longer imports scanner or calls system.out or .in
Pet only has state logic, calendar logic or dialogue text. nothing about how the text reaches the screen.
`readLineWithTimeout` takes a `BooleanSupplier` parameter rather than knowing about pets idle timer. The _policy_ (when is it idle) stays in `Pet`, the _mechanism_ (how to poll for input) lives in `ConsoleView`.
`showCalendarFor()` now builds the events into `view.println(event.toString())` calls rather than a raw `System.out.println(event)` — functionally identical, just routed through the view.

goToSleep() - goes to sleep and reset the date into one method instead of updating current date.


