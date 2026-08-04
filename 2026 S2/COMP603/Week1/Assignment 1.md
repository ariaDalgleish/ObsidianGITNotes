
Project: **Inventory Management System** or Card Game 
**Desktop Pet with daily calendar.**

Loop:
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
- Sync calendar to google or cloud calendar

![[canvas_desktop-calendar-pet-260722_0117 1.png]]

Assignment Overview:
Requirements of Assignment 1
• Object-Oriented (OO) Programming concepts must be applied to the project. Important OO concepts,
i.e., encapsulation, abstraction, inheritance and polymorphism, must be reflected.
• In Software Development Project 1, you will need to develop a Command-line User
Interface (CUI) version of the software product using Java Programming Language.
• In Software Development Project 1, you will need to apply ALL the fundamental OOP
concepts (abstraction, encapsulation, inheritance, polymorphism), try to follow the SOLID
design principles, create multiple classes with relationships, and use text files to store input
and output data from the program.
• The source code of Project 1 will be submitted by the end of Week 7.
• Refer to the important dates for the due date of both project assignments.
• The program needs to be bug-free and has robust error handling.
• You need to develop the projects by using NetBeans 28 and JDK25.
• The program should be easy to build and run without any manual configuration.
• You need to have an open mind about the functionality of your software project and try your
best to make your program robust, interesting, and easy to use.
• You may use the Java standard library and other external libraries.
• You are encouraged to learn more beyond the lectures and apply what you have learnt to the
projects. However, the project requirements stated in this document should be satisfied.
• You also need to include a short report, stating the project setup and the contribution of each
teammate (if you work in a group). If any team member gives less than 40% contribution/no
contribution in terms of coding, the student will be given a penalty or even fail the course. The
report should also include an AI usage log as an appendix and a one-page reflective summary
on AI use. See the AI Usage Documentation section for details.
• You need to record a short video (less than 5 minutes) using any tools (e.g., MS Teams) to
demonstrate your project AND explain the code. The recorded video must be included in the
submission.
• Read Marking Guideline carefully for the details.

Rubric:

User Interface
	The program can handle users’ inputs from the CUI properly. The interface is easy for users to interact with

File I/O and Collections
	The program input and output data from/to text files successfully. File I/O must contribute to the functionalities of the project. Use classes/methods taught in this paper are used to manage File I/O. Appropriate Collections are utilized in the program.

Software Functionality and Usability 
	The program is easy to compile and run without any manual configurations (e.g., setup input/output files, import .jar files, etc.). The program works as expected without any errors. The functionality of the program is easy to learn and follow. Complexity and robustness of the functionality.

Software Design & Implementation
	The program can be compiled successfully. The purpose of the code is easy to understand by reading it. OOP concepts (abstract, encapsulation, inheritance, and polymorphism) are well applied. Follow the SOLID design principles. The comments in the code are useful and appropriate. The program demonstrates code modularity and reusability. The code executes without runtime errors. The error handling is thorough and robust