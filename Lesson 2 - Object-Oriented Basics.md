Lesson two is all about “object-oriented programming” – defining classes, declaring objects (which are variables), and writing methods that make your objects do things.
Didn’t get much feedback on how long the lesson took last week. Please let me know. Otherwise I guess I’ll just assume they are too short 😊
You’ll need to understand the following concepts:
-	What is a class
-	What is an object, and the difference between classes and objects
-	What constructors are and how to use constructors
-	How to define a class (fields and methods)
-	What are some advantages of OOP?

This video does a pretty good walkthrough of a simple class. Set playback speed as you desire. https://www.youtube.com/watch?v=0NPR8GFHNmE
This page describes objects a little bit more theoretically, but provides examples as well. Read through section 2.9 – no need to go any further than that. I recommend doing the Youtube video first so you have a little bit more familiarity, then reading this page. https://www3.ntu.edu.sg/home/ehchua/programming/java/J3a_OOPBasics.html
 
Assignments
Object-oriented practice – no “general practice” this week, but a long first problem and a short second problem.
1.	Create a class called “FrcRobot”. Give the class six methods, all of which are things any* modern FRC robot could do, regardless of game. For example – “drive()”, “turnOff()”, “stop()”, etc. You can use the three methods I just listed if you want, but you still need to write them.

Each method needs to System.out something that indicates it has been called (e.g. “Robot driving forward.”)

At least two methods need to accept some kind of parameter. For example, you could do “drive(int distanceInches);” The parameter should be reflected in the output.
2.	Make sure your FrcRobot class has at least five variables as part of its definition, and use at least three data types. For example, you could do a “String allianceColor”, “boolean isOn”, etc. Just make sure that the variables could be relevant to any game. (E.g. no “isHangingFromAirship”)
3.	Add two more methods that update class variables. For example, if one of your variables is “boolean isOn”, you could do “public void togglePower()”, that checks what the current power state is, and sets it to the other state. Other variables might need you to take a parameter. For example, “public void setAllianceColor(String allianceColor)”. At this point your program should have at least eight methods!
4.	Add two more methods that return class variables. For example, “public String getAllianceColor()”. Now your program has at least ten methods.
5.	If you haven’t already, create a constructor method. Make the constructor able to set at least two of your class fields. It can set more than two if you want. Now you have at least 11 methods!
6.	In your program’s main method, declare an FrcRobot variable and make sure all your methods get called at least once.

7.	Create a new program called “FrcSteamworksRobot”. Give this class at least two methods and at least two class variables that are relevant to Steamworks. Give your class a constructor that can set both the class fields. In your main method, create an FrcSteamworksRobot object using your constructor, and call both your non-constructor methods.
