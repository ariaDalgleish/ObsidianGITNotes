## **Desktop Pet with daily calendar.**

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

| State    | CUI                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |     |
| -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --- |
| On run   | *Checks for calendar source*<br>*No calendar found* = "Import calendar URL to proceed..."<br>*Calendar found move to sleeping pet state + dialogue*                                                                                                                                                                                                                                                                                                                                                               |     |
| Sleeping | ""zzz..." Pet is sleeping shh, do you want to wake up pet? (Type anything)"<br>*User types something and enters -> Awake state*                                                                                                                                                                                                                                                                                                                                                                                   |     |
| Awake    | ""Mmmrm" Your pet wakes up!"<br>*If daily calendar is already displayed skip to drop menu*<br>*Display daily calendar* <br>"Date"<br>"Event"<br>*If no scheduled events found ->* "Nothing to do today!"<br><br>*Drop menu:*<br>"Type "Next" to view next day's schedule"<br>"Type "Back" to view previous day's schedule"<br>"Type "Reset" to view the current day."<br><br>*If user types unrecognized command*<br>""Hmmm?" Your pet tilts head in confusion"<br>*If user types command change state to active* |     |
| Active   | *Wipe CUI*<br>*Next command* "Pet flips calendar's page foward!"<br>*Back command* "Pet flips calendar's page back!"<br>*Reset command* "Pet flips calendar's page foward!"<br>*Display daily calendar* <br>"Date"<br>"Event"<br>*If no scheduled events found ->* "Nothing to do today!"<br>*Return to idle state*<br>                                                                                                                                                                                           |     |

