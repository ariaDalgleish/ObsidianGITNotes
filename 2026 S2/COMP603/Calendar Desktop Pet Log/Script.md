I started with the idea of developing a virtual desktop pet, but I thought it'd make for a much better project if it had a useful function.  
A virtual pet lets user interact to maybe give inputs, click buttons, play animations. I would want my virtual pet to display reminders for myself.  
I'm always using my calendar to keep track of my tight schedules of what's happening and where I need to be at what time.
So I decided I'd make a Virtual Calendar pet to display the date and events!

Here is my first mock up using Milanote to get a visual of what the application could look like and the different stages.
After trailing different ideas I decided to design my structure working around the pet's states of sleeping, Awake, and active. 
So I created a table to map out the different input and interactions with the pet to cycle through the states

Creating the project I ended with 9 classes that all work together using methods of abstraction, encapsulation, inheritance and polymorphism.

My calendar class structure works between 5 classes starting with CalendarSource which is the interface that lets my Pet class ask for events.
It only references CalendarEvent - an immutable event data.
CalendarSource then implements AbstractCalendarSource which handles shared parsing logic, storage and look up.
AbstractCalendarSource extends LocalFileCalendarSource. 
Which reads the calendar events from a local txt file or in future a given URL - and then hands them off to the parent.
AbstractCalendarSource throws or catches CalendarImportException. This class extends exception so the compiler will handle or declare any bad lines.

For my Pet class structure I've got my Petstate enum which abstracts what stage the pet is at into three clear possibilites.

My pet class is split with ConsoleView class handling inside logic while Pet only has state logic, calendar logic or dialouge text. Nothing about how the text reaches the screen.

Pet is my big class that calls for which state the pet should enter and all the interactions with user input. It also has a timeout function calling for pet to sleep after a certain time. Right now this is after 15 seconds just for easy testing.

And this is how it runs!