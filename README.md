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
## The most important thing is that:  
 If you're code is **clean**, you can catch bug **easily**.    
 If you're code is **dirty**, bugs will crawl *everywhere* !

### Let's explain it with a metaphor:
Let's say one day you saw a cockroach running in your room, because you hate it so you want to catch it.  Now imagine for 2 cases : 
- Case A : Your room is very tidy and clean
- Case B : Your room is very messy and dirty  

Now, for which case do you think it is easier for you to catch the cockroach?
Of course is Case A! 
So, this concepts also applies to coding. No exceptions.

# How to write **clean** code?
# Use good naming
### You have to know the naming convention  

| Type| Example| Languages that uses it|  
| ------------- |:-------------:|----------|
| snake_case| `int total_ticket_price = 0;` | C++, Python|
| CamelCase      | `int totalTicketPrice = 0;` |Java, C#, Javascript|
| kebab-case | `int total-ticket-price = 0;` | Lisp|  

So, the rule is: *always follow the convention*.  In the example below, we will be using C++ to demonstrates examples, so `snake-case` will be used throughout this documentation.
## **Don't afraid to type LONG names!**  
Now let's compare between bad name and good name.  

| Type    | Bad                                        | Good              | Reason                                                           |
|---------|--------------------------------------------|-------------------|------------------------------------------------------------------|
| int     | `tkt_cnt`                                  | `ticket_count`    | Variable name should be understandable during first read.        |
| string  | `universiti_tunku_abdul_rahman_student_id` | `utar_student_id` | Popular short form should be used when possible.                 |
| boolean | `finish`                                   | `is_finished`     | Boolean variable should be prefixed with 'is' and in past tense. |
    
## Function name should be meaningful  

| Bad function name | Good function name | Reason                                             |
|-------------------|--------------------|----------------------------------------------------|
| `menu()`          | `displayMenu()`    | Function name should be VERBS!                     |
| `check()`         | `checkBalance()`   | Function name should be as specific as possible.   |
| `func1()`         | -                  | WTH is func1? Function name should at least has some meaning.  |

## Don't use magic numbers!
```cpp
//Example of magic numbers
int total_sleeping_hours = sleeping_hours_per_day * 5; //What is 5?
```
```cpp
//How to avoid magic numbers
const int NO_OF_WEEKDAY_PER_WEEK = 5;
int total_sleeping_hours = sleeping_hours_per_day * NO_OF_WEEKDAY_PER_WEEK ; 
```
## How to use boolean properly
It is normal that beginners usually use boolean like the following :
```cpp
bool is_happy;
if(is_happy == true) printf("I'm happy");

bool is_sad;
if(is_sad == false) printf("I'm not sad");
```
There's actually a better way of doing it:
```cpp
bool is_happy;
if(is_happy) printf("I'm happy");

bool is_sad;
if(!is_sad) printf("I'm not sad");
```

# About GOOD functions
Before we talk about how to write good functions, let's look at the category of functions:  

| Type | Have to return something | Have parameters | Example                          | Comments                                            |
|------|--------------------------|-----------------|----------------------------------|-----------------------------------------------------|
| 1    | No                       | No              | `void say_hello();`              | Should only be used when I/O operation is involved. |
| 2    | No                       | Yes             | `void print_number(int number);` | Should only be used when I/O operation is involved. |
| 3    | Yes                      | No              | `int get_my_name();`             | Good.                                               |
| 4    | Yes                      | Yes             | `int add(int x, int y);`         | Very good.                                          |  

As you can see Type 3 and Type 4 functions are consider good, so most of your functions should be of these types.   
Moreover, you should avoid Type 1 and Type 2 functions whenever possible.  
## Avoid *Side Effects* if possible
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

## Single Responsibility Principle (SRP)
Now, let's talk about SRP. What is SRP? Basically it means ALL function should only handle ONE and only ONE job.
Let's look at an example that violates SRP:
```cpp
void get_average(){
    int number1;
    int number2;
    scanf("%d", &number1);
    scanf("%d", &number2);
    int result = (number1 + number2) / 2;
    printf("The average is : %d", result);
}
```
How does this code violate the SRP?  
Because it is doing THREE things : 
1. Get user input
2. Calculate the result
3. Print the result
  
So, how can we refactor this code so that it will follows SRP? Let's look below: 
```cpp
int get_number_from_user();
int get_average(int x, int y);
void print_result(int result);

int main(){
    int number1 = get_number_from_user();
    int number2 = get_number_from_user();
    int result = get_average(number1, number2);
    print_result(result);
}

int get_number_from_user(){
    int user_input;
    printf("Please enter a number > ");
    scanf("%d", &user_input);
    return user_input;
}

int get_average(int x, int y){
    return (x + y) / 2;
}

void print_result(int result){
    printf("The average is : %d", result);
}

```
## How to check whether my function is violating SRP?
- Check if your function is longer than one page, if it is, it is most probably violating SRP already
- Check if your function involve I/O functions such as `printf` and `scanf`
- Ask your friend if he/she can understand your code
    - if they can't understand your code properly, you're probably violating SRP already
    - because if you follows SRP all the times, your code should be very easy to read, just like reading *novel*.

## About loops
#### Use *INFINITE* loop and `break` instead of comparing to a boolean variable
```cpp
bool is_done = false;
while(!is_done) {
    int input = get_input();
    if(input == 0) is_done = true;
    else print(input);
}

// Below is a better way of doing it
while(true) {
    int input = get_input();
    if (input == 0) break;
    else print(input);
}
```
# About comments
## Don't comment unless neccesary
For example, below is an unecessary comment : 
```cpp
int x = 5; //create an integer variable
```
## Don't comment to explain what you're doing
```cpp
int x; //x is user choice

//display the menu
printf("Welcome to LOL, please select an option\n");
printf("Choice 1 : PLAY GAME");
printf("Choice 2 : Check highscore");
printf("Choice 3 : Quit");
printf("Enter your choice >> ");

//get the user input
scanf("%d", &x);

//check if user input is correct
if(x < 1 || x > 3) printf("Error!");

```
So, the example above is a bad example, now let's look at a good example:
```cpp
int user_choice;
display_menu();
user_choice = get_user_input();
check_for_error(user_choie);
```
So the trick here is, whenever you feel like  you want to comment, just make the section becomes a **FUNCTION** !

## So when should I comment?
- When you are documenting the code
- When you want to include license in the code
- When you want to write some TODO 
```cpp
//Example of TODO
int add_two_numbers(int x, int y){
    //TODO: Complete the code here
}
```
### Why do you need to use TODO?   
Because sometimes you might suddenly have inspiration for doing other codes in other files but you're afraid you will forget what you are going to do in the current file.

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

# To learn more about Clean Code ... 
Please read this book :  
![image](https://user-images.githubusercontent.com/23183656/31491338-94e1e938-af79-11e7-9468-c41325d75676.png)

The link for this book is [here](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882).

# Example of clean code
```cpp
#include <stdio.h>
/*
This is a code about a simple calculation program
that receive 2 numbers from user 
and print the sum of the numbers
*/

int get_number_from_user(){
	int result;
	printf("Enter a number >> ");
	scanf("%d", &result);
	return result;
}

int add(int x, int y){
	return x + y;
}

void print_result(int result){
	printf("The result is %d\n", result);
}

bool user_wants_to_continue(){
	char input;
	printf("Do you want to continue(Y/N)?");	
	scanf("%c", &input);
	if(input == 'y') return true;
	else return false;
}


int main(){
	while(true){
		int number1 = get_number_from_user();
		int number2 = get_number_from_user();
		int result = add(number1, number2);
		print_result(result);
		if(!user_wants_to_continue()) break;
	}	
}


```
More example:
```cpp
int get_ticket_type(){
	int result;
	printf("Choose a ticket type\n");
	printf("1. Child\n2. Adult");
	scanf("%d", &result);
	return result;
}

const int CHILD_TYPE = 1;
const int ADULT_TYPE = 2;
int main(){	
	while(true){
		int ticket_type = get_ticket_type();
		switch(ticket_type){
			case CHILD_TYPE: //do the things 
				break;
			case ADULT_TYPE: //do things
				break;
		}
	}	
}
```
# Thank you for reading! 
## If you like it please STAR this repository!
