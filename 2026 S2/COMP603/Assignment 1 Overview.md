
Assignment Overview:
#### Requirements of Assignment 1
- Object-Oriented (OO) Programming concepts must be applied to the project. Important OO concepts, i.e., encapsulation, abstraction, inheritance and polymorphism, must be reflected.
- In Software Development Project 1, you will need to develop a **Command-line User Interface (CUI)** version of the software product using Java Programming Language.
- In Software Development Project 1, you will need to apply ALL the fundamental OOP concepts (abstraction, encapsulation, inheritance, polymorphism), try to follow the SOLID design principles, create multiple classes with relationships, and use text files to store input and output data from the program.
- The source code of Project 1 will be submitted by the end of Week 7.
- Refer to the important dates for the due date of both project assignments.
- The program needs to be **bug-free** and has **robust error handling**.
- You need to develop the projects by using **NetBeans 28 and JDK25.**
- The program should be easy to build and run without any manual configuration.
- You need to have an open mind about the functionality of your software project and try your best to make your program robust, interesting, and easy to use.
- You may use the Java standard library and other external libraries.
- You are encouraged to learn more beyond the lectures and apply what you have learnt to the projects. However, the project requirements stated in this document should be satisfied.
- You also need to include a short report, stating the project setup and the contribution of each teammate (if you work in a group). If any team member gives less than 40% contribution/no contribution in terms of coding, the student will be given a penalty or even fail the course. The report should also include an AI usage log as an appendix and a one-page reflective summary on AI use. See the AI Usage Documentation section for details.

- You need to **record a short video** (less than 5 minutes) using any tools (e.g., MS Teams) to demonstrate your project AND explain the code. The recorded video must be included in the submission.
- Read **Marking Guideline** carefully for the details.

## AI Usage Documentation
As part of your project submission, you are required to include an AI Usage Documentation appendix in your project report. This component is worth 5 marks and consists of two parts.
### Part A – AI Interaction Log (Appendix A)
Include a table in the report summarizing the key interactions you had with any GenAI tool during the project. The table should have the following columns:

| Prompt                                                                                                                                                 | Tools Used | What AI Generated                                                           | What I accepted/modified/rejected                                                                                            |
| ------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| "Write a Java method that validates booking<br>start and end dates using `LocalDate`.<br>Throw an exception if the end date is before the start date." | ChatGPT    | A `validateDates()` method using `LocalDate` and `IllegalArgumentException` | Modified- `IllegalArgumentException`with our<br>custom `BookingException` class to match the project's error-handling design |

### Part B – One-Page Reflective Summary (Appendix B)
Write a short reflection (maximum one page) in your own words covering the following:
- **What** tasks you used AI for (e.g., code generation, debugging, design, naming, etc.)
- **Why** – what you were trying to solve or speed up
- **How** AI influenced your design choices – did you accept a suggestion, modify it, or reject it, and why?
- **What** the project gained (or did not gain) because of AI
- Honest acknowledgement of where AI was wrong or unhelpful
This reflection summary must be written in your own words. AI-generated text in the reflection
will result in zero marks for this component.

#### Submission:
ZIP folder contains:
1. The project folder with all the source codes and related files, e.g., image files, text files, unit tests, etc.
2. A short report, including:
	- the project setup (e.g., user name and password)
	- the contribution of each team member if this is group work (this item is not required if you work individually). If any team member gives less than 40% contribution/no contribution in **terms of coding**, the student will be given a penalty or even fail the course.
	- Appendix A: AI interaction log
	- Appendix B: One-page reflective summary on AI use
2. A short video (less than 5 minutes), including
	- Project demonstration, showing all the features by running your project
	- Code explanation, explaining class structures, methods and processes.
# Rubric:
#### *15%* **Labs**
Complete 3 

#### *15%* **User Interface**
- The program can handle users’ inputs from the CUI properly. 
- The interface is easy for users to interact with

#### *15%* **File I/O and Collections**
- The program input and output data from/to text files successfully. 
- File I/O must contribute to the functionalities of the project.
- Use classes/methods taught in this paper are used to manage File I/O. 
- Appropriate Collections are utilized in the program.

#### *20%* **Software Functionality and Usability** 
- The program is easy to compile and run **without any manual configurations** (e.g., setup input/output files, import .jar files, etc.). 
- The program works as expected without any errors. 
- The functionality of the program is easy to learn and follow.
- Complexity and robustness of the functionality.

#### *30%* **Software Design & Implementation**
- The program can be compiled successfully. 
- The purpose of the code is easy to understand by reading it. 
- OOP concepts (abstract, encapsulation, inheritance, and polymorphism) are well applied. 
- Follow the SOLID design principles. 
- The comments in the code are useful and appropriate. 
- The program demonstrates code modularity and reusability.
- The code executes without runtime errors. 
- The error handling is thorough and robust
- The class structure reflects good design

#### *5%* **AI Usage Documentation**
- The submission includes an AI Interaction Log with specific prompts and clear descriptions of what was accepted, modified, or rejected
- The AI Interaction Log is consistent with the AI- related comments in the code.
- A one-page reflective summary is included, written in the student's own words.
- The reflection discusses how AI was used, how it influenced design or implementation decisions, and demonstrates critical thinking about AI outputs.