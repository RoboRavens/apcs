Lesson 12 – String Parsing
	“Parsing” is the act of taking some value, often a string but occasionally in some other format such as a number, and searching it for certain parts or sections, which you would then do something with. For example you might want to replace a portion of a string with a different string, or pull a specific value out, or make certain characters uppercase.
	Some examples (these aren’t problems for you to solve, just things that someone hypothetically might want to solve):
-	Parse the day of the month out of the string “September 14th, 2017”
-	Replace the first letter of each word with a capital letter in the string “this was supposed to be in title case”
-	Replace the token “[name]” in the following string with the text “Peggy”: “I am going out to lunch with my coworker [name] and will be back at 1:00.” (A token is some known quantity in a string that you can search for, typically to make parsing or replacing easier.)
-	Return just the values after the decimal point in “3.1415”
Sometimes you may also want to parse something with a known format for a number of values. Consider a text file with the following contents:
1188,.82,x
2767,.96,x
33,.7,20
67,.9,x
217,.85,x
4362,.4,10
This is a translation of the robot and manipulator values I used for my Steamworks3v3s game. We could parse this is a predictable way by saying “find the first comma, and take the value up until that point. That is the team number. Then take the value between the first and second commas, and that is their manipulator success probability. Then take the value from the second comma to the end of the line. If it’s an “x”, make a GearPlacer. Otherwise make a FuelShooter and that number is the number of fuel it shoots. After you reach the end of the line, start over on the next line.” 
In our Steamworks3v3 class we had methods for creating the red and blue alliances that had hard-coded values for the robots, but with string parsing, we could read in a file generate alliances based off the contents. This would allow our program to run for any combination of alliances instead of needing to be updated for each one. For example, given an event match schedule, we could generate a text file with all the matches, give it to our program, and simulate every single match!
String parsing isn’t a huge aspect of robot code because robot code doesn’t have that many strings, but it’s a massive part of most other kinds of programming (desktop application, web-based, etc.) There are built in methods in Java to make it easier for you (in the old days you had to turn every string into, basically, an array of letters, and iterate through the array repeatedly to do things) that are methods for String objects. Some of these are included on the AP test so we’ll learn them. String parsing can be a pain sometimes, but it’s actually not too difficult once you get the hang of using the methods.

Explorations
For the exercises for this project, you’ll spend some time exploring the String object methods in Eclipse.
1.	Create a new Java project; doesn’t matter what it’s called. In your main method create a String variable and assign it some value. Again doesn’t matter what it’s called. I’ll refer to mine as “test”.
2.	Type “test.” on a new line of code so that Eclipse pulls up a list of methods. Scroll through the list of methods and read the descriptions for the following methods. Make sure you look closely at the method signatures below – many methods have overloads that take the same number of arguments, but a different kind of variable. 
a.	length()
b.	charAt(int)
c.	indexOf(String)
d.	indexOf(int, String)
e.	lastIndexOf(String)
f.	replace(String, String)
g.	split(String)
h.	substring(int, int)
i.	toLowerCase()
j.	toUpperCase()
3.	As you can see, there are a ton of methods, some more useful than others. SOP an example of you using each method. You don’t need to do anything specific, but your SOP should output something – not a blank line. A good value that you can set your test string to use each method is “tes,12test,8jastes|,,asdatest.,” (That’s not a typo.)
4.	Now some more specific exercises. Use appropriate string parsing methods for each.
a.	Print the length of the string “The length of this string is “The length of this string is 32.”
b.	Print the 14th character of the above string, sing the charAt.
c.	Using the same string,  print the number of characters that appear before the word “string”.
d.	Print the number of characters that appear before the second “i”.
e.	Print the number of characters in the string after the last “g”.
f.	Replace the word “string” with the word “text”.
g.	Replace every “n” with a capital N.
h.	Using the string “10,20,30,40,50,60,70,80”, print each of the numbers in the string, but none of the commas. (Use the split method.)
i.	Print the “the length of …” string used above in both upper case and lower case.
 
Lesson 12 – String Parsing – Part Two
	Lesson 12 part one used an example of SteamworksRobot objects, from your Steamworks3v3 project, being described by a String like so:
1188,.82,0
2767,.96,0
33,.7,20
67,.9,0
217,.85,0
4362,.4,10
In this example, the first number is the team number, the second number is the scoring probability (either gears or per shot of fuel) and the third value either the number of fuel per shot, or the number zero, if the robot is a gear manipulator. (If the third value is higher than zero, the robot is fuel shooter.)
Steamworks robot strings could be combined and delimited (separated by a known value) by a pipe character | like so:
1188,.82,0|2767,.96,0|33,.7,20|67,.9,0|217,.85,0|4362,.4,10
Accordingly, an alliance of three robots would look like this:
1188,.82,0|2767,.96,0|33,.7,20
In your Steamworks3v3 game, in your createRedAlliance and createBlueAlliance methods, you currently hardcode values for the gear and fuel robots. Modify these methods such that they parse a string of this format to create the robots instead.
Accordingly, at the start of each of these methods, there should be a string declaration along the lines of:
String robots = “1188,.82,0|2767,.96,0|33,.7,20”;
Followed by parsing code to turn the numbers into variables. For each alliance, you can just declare nine variables (six integers and three doubles) to store the values. 
In order to turn strings into ints or doubles, you will want to use the following static methods:
	Integer.parseInt("1188");
Double.parseDouble(".7");
These methods take a string argument and return an integer or double value, respectively. So parse the string value, and then use these methods. Once you’ve parsed the values, create your manipulator and robot objects. Note that you will now need an if statement when creating GamePieceManipulators, because you have to check the fuel shot per attempt variable to determine whether it is a gear robot or a fuel robot.
When you’re done, your program should function the same as it did before, but instead of having hardcoded values in your createRed/BlueAlliance methods, you’ll have string parsing. Next week, we will make expand upon this functionality such that you can read values in from a file. 

