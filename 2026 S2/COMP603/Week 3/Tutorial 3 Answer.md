Task 3.1 what  is the output from the following code? (PLQuiz)
```
str 1: Hi aInt 1: 0
str 2: Hi ,how are you aInt 2: 12
```

Task 3.2 (submission requirement)

Develop math quiz program which can interact with a user via a command-line user interface (CUI). It can randomly generate a math question and check whether the user can provide the correct answer.
- Randomly generate 2 integers between 0 to 100
- Randomly generate a math operation from + , - , * and /
- Display a math question by using the generated numbers and operator in steps 1 and 2, e.g. 22 * 45
- Prompt the user to input the answer from the command line based interface
- If the user inputs and invalid input (e.g. a string), prompt the user to input again.
- If the user's input is valid, verify whether the answer is correct. If it is correct, award the user 10 points; otherwise, deduct 10 points from the user's score.
- Quit the game if the user inputs an 'x' as the answer to a question.
- Display the user's total score and quit the program.
Use methods in java.util.Random to generate random numbers.

Task 3.1 PLQuiz uses a mutable QuizState object (like ResultString) passed into methods so you can observe how object fields change while reassigning the parameter inside a method doesn't affect the caller.

both main and changeData use static
static means this belongs here.