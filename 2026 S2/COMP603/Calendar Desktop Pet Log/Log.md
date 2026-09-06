## **Desktop Pet with daily calendar.**

Pet States:
1. Sleep/Idle 
	1. Pet is sleeping or playing idle animation, the application is running in background to save power and memory it is limited to very small run time
2. Active
	1. By mouse clicking on the virtual pet, the pet "wakes up" with an alerted animation and the application is now fully interactable. 
	2. Two buttons "pop" out (left arrow key button and right arrow key button), these buttons control the calendar pages. The buttons are interactable through mouse click input on the button, or by pressing the keyboard arrow keys. 
		1. Left arrow button flips the page over to show the previous day
		2. Right arrow button flips the page over to show the next day.
	3. The calendar widget displays a short summary of the date and the events.  
		1.  Have way for player to import calendar link that's easy to use and understand.
		2. Code implements calendar web url
3. Sleep/Idle
	1. After a certain amount of time and the pet has not been interacted with, the application will return to sleep mode until woken -> active.

**How to flip pages back and forth?**
- Main interaction - mouseclick
- Mouse click then activates virtual pet from idle (sleep)
- Once active different interaction buttons are unlocked:
- Pop up buttons of keyboard inputs that also use mouse click interaction.
 **Calendar setup**
- Have way for player to import calendar link that's easy to use and understand.
- Code implements web url.
 **Idle / Sleep saves computer performance since it'll run in the background.**
- Restricted inputs to make project achievable.
- Implements both mouse and keyboard inputs.
- Sync calendar to google or cloud calendar or any URL 

![[canvas_desktop-calendar-pet-260722_0117 1.png]]

https://youtu.be/il7eVsDPFoA?si=uZeX4i8OzUCL2cPX

 Class Calendar.Builder
[java.lang.Object](https://docs.oracle.com/en/java/javase/25/docs/api/java.base/java/lang/Object.html "class in java.lang")
	java.util.Calendar.Builder



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


https://github.com/openjdk/jdk/blob/master/src/java.base/share/classes/java/util/Calendar.javahttps://docs.oracle.com/en/java/javase/25/docs/api/java.base/java/util/Calendar.Builder.html

Old ^^ 
Stick to java.time package and friends.

I don't want the calendar to be interactable just to display information from an already made calendar such as date and scheduled events for the day. Only interactable functions will be to change the day to previous or next day, and a settings to import calendar URL.