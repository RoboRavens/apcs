	This lesson is just review and isn’t intended to take as long as the previous lessons. I have some short answer questions for you. Please answer them in your own words. Explaining a concept reinforces understanding.
	For submission of short answer questions, you can save them in a document if you wish, or just answer them in an email to me. Whatever suits you. Like with the code assignments, I may ask you to change or rewrite your answer if it is missing a key concept. Whatever format you choose, please label your answers with question numbers.
	Protip: I double checked, and the answers to all of these questions are either provided in my lesson documents or the linked resources. If you’re unclear on what a question is asking, please ask for clarification.
	After the short answers, there is the beginning of the project I originally was going to assign for this lesson. I think the project will be kind of fun, but it might take a little while and I didn’t want you guys worrying about that while also working on lesson 3 resubmissions. So now we’re going to split it into two lessons. For this one, you’ll just start by defining some of the easier parts, and then for lesson five you’ll have that out of the way to focus on the more difficult parts of the project. Good job so far, I’m happy with the level of effort everyone is putting in and also the level of understanding. You’re all doing very well.
-------
Short Answer Questions
1.	What is a “nested” loop? Provide an example of when you might want to use a nested loop.
2.	Explain what “constructors” are and why they special, in about three sentences.
3.	What does it mean to “overload” a method? List the three different possible ways you can change a method declaration to differentiate it.
4.	How is an “object” different than a “class”?
5.	List two advantages of using object-oriented programming, as compared to programming without classes or objects.
6.	What does it mean when a class variable or method is “private”?
7.	What syntax keyword do you use to declare that a variable is a constant?
8.	Assume you are working on a program that has a class called “BoulderShooter”. BoulderShooter does not have any constructors defined for it other than the default constructor. Write a line of code that would create a new BoulderShooter object.
-------
Code Project
We’re going to make a turn-based Steamworks game simulation. I hope you have some fun with this. Please read the instructions carefully. This is almost a tutorial, and I think if you follow along this shouldn’t be too hard (there will be some challenging parts.) If you don’t follow the tutorial, it could be very difficult. For reference, I did this assignment myself, and it ended up being about 250 lines total. (Since we’re only starting the project right now, you’ll have way fewer than 250 lines when you finish this assignment.) Yours will vary, but that’s an idea of how much code we’re looking at.
This game is going to be pretty simple – the user will be able to start a new game, and during the game, they can select an action each turn. Every turn takes five seconds off the clock. Eventually the clock hits zero and the game ends. All we’re going to do is track the number of gears/rotors each alliance scores, and the number of fuel. We won’t factor in autonomous points or penalties, and we won’t worry about individual robots – just the red and blue alliance. We will assume that the pilot scores the free gear. We’ll also keep track of whether or not each alliance gets the bonus. We’ll pretend it’s an elimination match, so they get a flat number of points added to their score.
Note that in software, there are always a number of different ways to approach a problem. This tutorial is not the only way to implement this game, and arguably not even the “best”. However, it is an acceptable way that only uses topics that we have learned so far.
1.	In Eclipse create a new project called SteamworksSimulator.
2.	Create a class called “SteamworksSimulator”. Check the box to put your main method here. Every method in this project will be public.
3.	One of the purposes of this project is to show you how the main class can be used solely to kick off a program, but none of your logic needs (or should) go there. Paste in the following code to your main method – this is it; you should not add any more code to your main method, or the SteamworksSimulator class, for the entire project.
public class SteamworksSimulator {
	public static void main(String[] args) {
		SteamworksGame steamworksGame = new SteamworksGame();
		steamworksGame.start();
	}
}
4.	Let’s fix the syntax errors. Add another class to you to your project called “SteamworksGame”. Add a method called “start” to fix the syntax error in your main method. It can be empty for now. It doesn’t need parameters and will not return anything.
5.	There are a number of Steamworks-related things we’re going to need to know and use in order to write this program. We’re scoring gears and fuel. Gears turn into rotors, but not at a constant rate. Fuel and rotors are worth different point values. And we need to keep track of how many of each need to be scored to get the bonus, and what the bonus is worth. Let’s declare a few constants in your SteamworksGame class. Declare the following constants in your SteamworksGame class:
a.	Number of gears needed to spin each rotor
i.	First rotor is 1
ii.	Second rotor is 2
iii.	Third rotor is 4
iv.	Fourth rotor is 6
b.	Points for each rotor = 40
c.	Fuel per point = 3
d.	Fourth rotor bonus = 100
e.	Forty kPa bonus = 20
f.	Game duration in seconds = 150
6.	We’ll also need a few variables to keep track of the game state. Declare the following variables in your SteamworksGame class:
a.	The number of gears the red alliance has scored
b.	The number of gears the blue alliance has scored
c.	The number of fuel the red alliance has scored
d.	The number of fuel the blue alliance has scored
e.	The number of seconds that have elapsed since the start of the game.
7.	Note that none of the variables are for the scores of the alliances. While we could make variables for these, it wouldn’t do us a lot of good, because we would still need to keep track of the components. Otherwise there would be no way to tell when the next rotor is going to spin or if an alliance has achieved the fuel bonus. Later on we will write code that uses the components to calculate a final score. Since we’re going to write a method that exposes the final score, and we want to manage these variables carefully, let’s set them all to private.
8.	Our game is going to need a user interface. I don’t want you to spend a ton of time making one, so just copy these methods, and paste them into SteamworksGame:

public void displayWelcomeMessage() {
		System.out.println("Welcome to the Steamworks Simulator.");
	}
	
	public void displayMainMenu() {
		System.out.println("Enter a number to perform an action.");
		System.out.println("1: New game of Steamworks");
		System.out.println("2: View session high score.");
		System.out.println("3: Exit program.");
	}
	
	public void displayGameMenu() {
		System.out.println("1: Place a gear for red");
		System.out.println("2: Place a gear for blue");
		System.out.println("3: Score ten fuel (high boiler) for red");
		System.out.println("4: Score ten fuel (high boiler) for blue");
		System.out.println("5: Conserve battery power");
		System.out.println("6: Skip to end of game");
	}

	public void displayExitMessage() {
		System.out.println("Thanks for playing Steamworks!");	
	}
9.	

At this point, you should have two classes in your project. There should not be any syntax errors, though the program will not do anything when you run it. You should additionally have nine class constants and five class variables defined in your SteamworksGame class, plus the methods above. That’s all for now – next lesson, we’ll make the logic methods that make the game actually do something.
