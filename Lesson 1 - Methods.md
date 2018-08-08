For the first lesson we're going to take a closer look at methods (sometimes referred to as "functions") in Java. Remember, methods are basically self-contained chunks of code that can be called in some other location, so the code doesn't need to repeated. There are built-in methods (for example System.out.println) and you can also write your own methods.
Please do me a favor and keep track of how long it takes you to complete this lesson, including the learning part and the problems. I will use your feedback to make sure lessons and problem sets are of appropriate length going forward.
I recommend you start early.

You'll need to understand the following concepts:
- What is a method
- Difference between built-in methods and methods you create for yourself
- Advantages of methods/why use them
- What method parameters/arguments are and how to use
- How to return data from a method, and how not to (the "void" keyword)

You do NOT need to worry about the "public" or "static" keywords you often see before method names.

This page has a good overview of methods. Please read all six of the links. Don't worry, each page is pretty short. https://mathbits.com/MathBits/Java/Methods/methods.htm

Additionally, here is a video that explains methods and demonstrates some capabilities. https://www.youtube.com/watch?v=-IJ5izjbWIA Note: I will link a lot of youtube videos. Take advantage of the option to change the video speed by clicking on the gear in the lower-right corner. If the topic is confusing, you can run it slower. If it's making sense, you can save yourself time by running it faster.

After you've covered methods, watch the following video about variable scope: https://www.youtube.com/watch?v=Y2iN3TO5qOQ

"Scope" is the concept of where a variable exists and for how long. Basically, variables declared in a method only exist in that method, variables declared in a loop only exist in that loop, and variables declared in a class exist throughout that entire class. A variable cannot be accessed or changed from a location in code where it does not exist.

## Using the Java Scanner class to get user input

Java has a "Scanner" class that can be used to get user input from the console that appears at the bottom of your Eclipse screen where your program output is. Here's an example of how to use it to get an integer.

```
import java.util.Scanner;

public class Main {

	public static void main(String[] args) {
		System.out.print("Enter a number: ");
		Scanner scanner = new Scanner(System.in);  
		int userInput = scanner.nextInt();
		System.out.println("You entered " + userInput);
		scanner.close();
	}

}
```

This declares an integer variable called "userInput" and it will take the value of whatever you enter into the console. Using the scanner will pause your program until you enter something and press enter. If you enter something that isn't an integer, you'll get an error. Make sure to familiarize yourself with the scanner because we'll be using it extensively.

## Assignments

Method-specific practice - if you get stuck on this assignment, refer back to the youtube video about methods. It should be helpful. Write a program that uses the scanner class to accept two integers from the user. For example:
```
Scanner scanner = new Scanner(System.in);
int firstNumber = scanner.nextInt();
int secondNumber = scanner.nextInt();
```

Then add six methods to your program as follows.
  1. A "welcome" method that takes no parameters and returns nothing, that outputs a simple "Welcome to calculator" message to the user.
  2. An "add" method that takes two integer parameters, adds the two integers together, and outputs the result. This method does not return anything.
  3. A "multiply" method that takes two integer parameters, multiplies them together, and then returns the result as an integer.
  4. A "subtract" method that takes two integer parameters, subtracts them, and then returns the result as an integer.
  5. A "modulo" method that takes two integer parameters, performs modulo division on them, and then outputs the result. This method does not return anything.
  6. A "cube" method that takes a single integer parameter, cubes it, and returns the result as an integer.

Then, in your main method, call each of these six methods using one or both of the numbers that the user input. For the methods that return a value instead of outputting a result, output the value they return in your main method. You can either use a variable to do this like so:
```
int product = multiply(firstNumber, secondNumber);
System.out.println(product);
```
Or you can combine that into a single line:
```
System.out.println(multiply(firstNumber, secondNumber));
```
So when you're done and you run your program, it should ask for two inputs, and then have six lines of output.

## General practice

  The hardest part is usually figuring out how to start. Consider what variables and loops you will need. Figure out the logic of how to solve the puzzle before you worry about writing code. If you spend ten minutes on problem and haven't made any headway, ask for help. Don't spend an hour - that just leads to frustration.
  1. Take an integer input from the user and compute the "sum of squares" from 1 to that number. For example if the user entered 10, the answer would be 1^2 + 2^2 + ... + 10^2. Output the answer. To check your work - if you enter 10, the answer should be 385. If you enter 11, it should be 506.
  2. Take an integer input and compute the "square of sum" from 1 to that number. So if they entered 10, it would be (1 + 2 + ... + 10)^2. Output the answer. To check - 10 comes out to 3025, and 11 comes out to 4356.
  3. Now calculate the "sum-square difference" - that is, the difference between the square of sum and the sum of squares. So basically, the the result of problem 2 minus the result of problem 1. If you enter 100, the answer should be 25164150. (Project Euler #5)
  4. Output a multiplication table for 1-10. Note that in order to do this you will need to do something a bit new - a "nested" loop. You'll have one for loop that goes from 1 to 10, and then you'll have another for loop that also goes from 1 to 10 inside the first for loop. Your nested for loop will complete fully for every cycle of the outer loop. Remember that you can use System.out.print instead of .prinln to output something without a new line, and you can do System.out.println(""); to output a new line and nothing else. So your result should look something like this (I'm not too concerned with the spacing):
  1 2 3 4 5 6 7 8 9 10
  2 4 6 8 10 12 14 16 18 20
  3 6 9 12 15 18 21 24 27 30
  .....
  10 20 30 40 50 60 70 80 90 100
