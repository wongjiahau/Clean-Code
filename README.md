# What is clean code?
![image](https://user-images.githubusercontent.com/23183656/31388542-061e820c-ae01-11e7-9e63-1071116d7716.png)

# Why write clean code?
*“Anyone can write a code that computer can understand.  
But only good programmer can write a code that human can understand.”*

Do you know who will be the victim of *dirty* code?   
### **YOU!**

Because you will be the one who read the code in the future.  
You will be cursing yourself like : 
```
What the heck is this?
What does that mean?
Is this comment important?
```
# How to write **clean** code?
# Use good naming
### You have to know the naming convention
| Type| Example| Languages that uses it|  
| ------------- |:-------------:|----------|
| snake_case| `int total_ticket_price = 0;` | C++, Python|
| CamelCase      | `int totalTicketPrice = 0;` |Java, C#, Javascript
| kebab-case | `int total-ticket-price = 0;` | Lisp
## **Don't afraid to type LONG names!**
Now let's compare between bad name and good name.
| Type    | Bad                                        | Good              | Reason                                                           |
|---------|--------------------------------------------|-------------------|------------------------------------------------------------------|
| int     | `tkt_cnt`                                  | `ticket_count`    | Variable name should be understandable during first read.        |
| string  | `universiti_tunku_abdul_rahman_student_id` | `utar_student_id` | Popular short form should be used when possible.                 |
| boolean | `finish`                                   | `is_finished`     | Boolean variable should be prefixed with 'is' and in past tense. |
## About loops
#### Use `break` instead of comparing to a boolean variable

## Function name should be meaningful
| Bad function name | Good function name | Reason                                             |
|-------------------|--------------------|----------------------------------------------------|
| `menu()`          | `displayMenu()`    | Function name should be VERBS!                     |
| `check()`         | `checkBalance()`   | Function name should be as specific as possible.   |
| `func1()`         | -                  | WTH is func1? Function name should at least has some meaning.  |

## Don't use magic numbers!
```cpp
//Example of magic numbers
int total_sleeping_hours = sleeping_hours_per_day * 7; //What is 7?
```
```cpp
//How to avoid magic numbers
const int NO_OF_DAY_PER_WEEK = 7;
int total_sleeping_hours = sleeping_hours_per_day * NO_OF_DAY_PER_WEEK; 
```


## About comments
### Don't comment unless neccesary
For example, below is an unecessary comment : 
```cpp
int x = 5; //create an integer variable
```
### Don't comment out useless code, just delete them
```cpp
```

### Don't use comment to explain what you are doing

## About functions
### Function should be one page long only

## Single Responsibility Princile
## Side Effects
```cpp

//This function have side effects
//Because it is calling I/O functions
int say_hello(){
    printf("%d", y);
}

int x = 5;

//This function have side effects
//Because it is using out-of-scope variable
int perform_random_math(){
    int y = x + 5;
    return y;
}

//This function have no side effects
//Because it is not calling any I/O functions
//And it is not using any out-of-scopt variable
int GetNumber(){
    return 5;
}
```

### We should avoid side effect whenever possible
The reason is simple, when we have as less side effects as possible, we can catch the bug easily.
  
  On the other hand, if we write a lot of function which have side effects. I assure you, there will be a LOT of bugs flying in your program.

# Utilize the editor
## Use shortcuts 
There a tons of shortcut available for each type of text editor.   
For example, the full list of shorcuts for Microsoft Visual Studio can be found here https://msdn.microsoft.com/en-us/library/da5kh0wa.aspx.
## Don't format the code yourself
Press the following key : 
```
Ctrl+K Ctrl+D
```
## Use the Light Bulb!
![image](https://user-images.githubusercontent.com/23183656/31390266-03665594-ae06-11e7-991c-1f301c72f3c7.png)

This is especially useful to help you to create methods.

# Use Google and StackOverflow
Whenever you face a problem, don't give up.   
Just copy the error and search it in Google.  
Most probably StackOverflow will have an answer for that.
