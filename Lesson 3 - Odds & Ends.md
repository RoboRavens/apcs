For lesson 3 we’re going to fill in some gaps and clarify a few things you’ve been seeing but probably don’t fully understand yet. Specifically, we’ll cover:
-	Method “overloading”
-	Access modifiers for methods and variables, and “information hiding”
-	Constants (like variables, except their value can’t change)
We’ll revisit getter and setter methods, and the additional context will explain why we use them instead of just updating the variable directly (e.g. frcRobot.isOn = true.)
Refer back to the same document about OOP from last week, but this time read sections 2.10 through 2.16: https://www3.ntu.edu.sg/home/ehchua/programming/java/J3a_OOPBasics.html#zz-2.10
Two videos instead of one, but each of them are short.
Overloading: https://www.youtube.com/watch?v=Cy5U6vjs848
Access modifiers: https://www.youtube.com/watch?v=ePj64t65G40 
Quick overview:
-	“Overloading” is when you declare methods with identical names, but different parameter lists. This lets you handle different situations with the same method, instead of writing a bunch of methods with different names. The document provides a good example of this.
-	Access modifiers: this will explain why you see the word “public” everywhere, and why getter and setter methods are used. Basically, you can use “public” and “private” to modify where a variable or method can be accessed.
-	Constants: if the value of something never changes, this lets you declare it and never have to worry about it somehow being updated. An example of this would be mathematical values (e.g. pi), or in our case, perhaps the diameter of a robot drive wheel. We want to use the value to calculate drive distance, but it should never change.

Assignment
For this assignment, you’ll modify your existing FrcRobot and FrcSteamworksRobot classes.
1.	Update your FrcRobot class such that ALL of its class fields are private. Note that this may give you syntax errors in your main method, because you can no longer access those variables from outside the class. Don’t worry about these errors just yet. If you want to be able to run your program, you can comment them out. (If you happened to never access any class variables from inside your main method, you won’t get any errors.)
2.	Update your FrcRobot class such that every class variable has both a getter and setter method. Depending on how you implemented FrcRobot last week, this likely means you’ll need to add several new methods.
3.	Now, in your main method, wherever you assigned one your FrcRobot variables, instead call a setter method to set the value. 
4.	Create an additional method in your “main” class (the class where your main method is) that calls all the getter methods of your FrcRobot class, and then SOP’s (System.out.println) their return values. Note that when you declare the FrcRobot object in your main method, it exists only in that method. So you will need to pass it to this additional method you are creating. So it will look something like this:
	public static void main (String args[]) {
		// Main method
		// Do stuff

		FrcRobot robot = new FrcRobot();
		// Do other stuff
		
		callGetMethods(robot);
	}

	public void callGetMethods(FrcRobot robot) {
		System.out.println(robot.getAllianceColor());
		System.out.println(robot.getDistanceTraveled());
		// etc., for all your get methods.
}
5.	Create an overloaded constructor in your FrcRobot class. Your class already has a constructor, and it takes at least two arguments. So for your overloaded constructor, simply change the number of arguments it takes. It could even take zero arguments. However, if you choose to make one with zero arguments, please also make a third one. So when you are done, your FrcRobot class will have at least two constructors that take at least one argument.
6.	In your main method, make sure both of these constructors get used. Your existing FrcRobot object should be creating using one of them. In order to use the new one, declare another FrcRobot object.
7.	Create a constant integer field in your FrcRobot class, for example “numberOfWheels”. Give it a value. You do not need to output this field anywhere; just create it.
8.	Switching over to the FrcSteamworksRobot class, perform similar steps:
a.	Make all the class variables private.
b.	Create getter and setter methods for each variable.
c.	In the main method of the program containing your Steamworks robot, use setter methods to update the class variables, and then use getter methods to output the values. (You don’t need to create the additional method like you had to in step 4 above, but you can if you want.)
d.	In FrcSteamworksRobot, create an additional constructor, and in your main method, create a second FrcSteamworksRobot object that uses the new constructor.
