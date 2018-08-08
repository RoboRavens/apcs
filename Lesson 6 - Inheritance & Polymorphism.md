	I hope that writing a real program gave you some insight into how some of the different things we’ve discussed can be used. I think it also demonstrates that the concepts you’ve learned so far are enough to start doing powerful things.
	This lesson is going back to the more regular format of new concepts and some smaller exercises. We’re going to dive deeper into object-oriented programming and discuss some more concepts:
-	Composition
-	Inheritance (extension)
-	Polymorphism
Composition is pretty simply – it’s simply the idea that a class can be composed of other classes. That means that when you’re defining variables in your class, you can use other objects. For example, if you had a BoulderShooter class and were making a class called StrongholdRobot, StrongholdRobot could have a BoulderShooter variable as one of its class fields. That’s really about all there is to it. It’s easy but it’s also critically important, because if we couldn’t compose classes with other classes we would lose a lot of reusability. After all, I want to be able to reuse BoulderShooter in our code for the 2019 game, FRC RockFight. But if StrongholdRobot couldn’t have a BoulderShooter object in its definition, we would have had to program BoulderShooter’s functionality right into StrongholdRobot.
Inheritance is the idea that you can define a class (called a “subclass” or “child” class) which has all the characteristics of a “parent” class, and then more. If you have a lot of classes which share common functionality, this is super useful, because that way you don’t need to re-write the same functionality. An example of this would be our robots each year. Every year, our robots need, for example, methods to run autonomous mode, run teleop mode, etc. Instead of redefining these methods every year, we can inherit them from a single parent class. In fact, this is literally how the field system works – FRC provides a parent class called robot, and every team’s code extends it. One thing that is critically important is that a class that inherits a variable or method can override that variable or method. For example, the default run teleop mode method that FRC provides literally does nothing. That wouldn’t be a very good robot, so we override it with our own method that does something. So every single different class that inherits from any given class could all have different implementations for a given method.
Polymorphism – fancy word for an important concept. It basically means that an object of a certain class can exist as a few different kinds of objects. For example, take an object that we know is a Robot. If we inherited the class Robot as described above, we could have made a class called SteamworksRobot, StrongholdRobot, or RockFightRobot. All of them are robot objects, even though they are different classes.
For an example of this, again think of the concept of an FRC field, running six different teams’ code. Our robot class is not going to be the same as 33’s, and theirs won’t be the same as 469’s. If the field was looking for a specific kind of robot, it would never be able to run everyone’s code. However, by defining a base robot class, and letting each team extend it, the field knows that every team’s robot class is a robot, and it has all the default functionality of a robot (because it inherited it), but it also has extra functionality.
Another example might be a superclass called “Vehicle”, and subclasses called “Truck”, “Boat”, “Rocket”, etc. As long as those classes inherit from vehicle, they have all of vehicle’s traits and can be used anywhere a vehicle could be used. So say vehicle has a “go()” method – all of these subclasses will have a go method, but that method could be defined differently for every single class. This lends a lot of flexibility to programs.
Ok – source material for this lesson. Go through sections 1-4 here: https://www3.ntu.edu.sg/home/ehchua/programming/java/J3b_OOPInheritancePolymorphism.html
There is a little bit less text for these sections than they had for the previous sections, so you might need to spend a little bit more time looking at the code they provide to see what they are doing. The examples are good. 

Assignment
1.	Create a new project called RobotComposition and create the following classes:
a.	Robot
b.	GamePieceManipulator
c.	RecycleRushRobot
d.	StrongholdRobot
e.	SteamworksRobot
f.	Elevator
g.	BoulderShooter
h.	FuelShooter
i.	RobotComposition, which will contain your main method
2.	In your robot class, define a class field called “manipulator”. Make its variable type “GamePieceManipulator”.
3.	In your RecycleRush, Stronghold, and SteamworksRobot classes, use the extends keyword to make these classes inherit from the class “Robot”. I will refer to these three classes – but not Robot itself - as “game robot classes”, just for ease of typing.
4.	Make your Elevator, BoulderShooter, and FuelShooter classes extend the class “GamePieceManipulator”. I refer to these three classes – but not GamePieceManipulator itself - as “manipulator classes”.
5.	In each of your game robot classes, create a constructor method that has no parameters. Inside your constructor, create an object of the class of the manipulator that best corresponds to that game. Then set the game robot’s manipulator class field (which it inherited from Robot, and therefore you don’t see in the code file you’re looking at), to the newly created object. Note how the “manipulator” variable is of type GamePieceManipulator, but across our three game robot classes, we were able to set it equal to objects of three different classes. That is because all of these classes, despite being different from each other, are still GamePieceManipulators.

Example: RecycleRushRobot constructor. Note how we can set this.manipulator, despite it not being defined inside of the file. 


6.	Go into GamePieceManipulator and create a method called “manipulate” that SOP’s some message.
7.	Go into Robot and create a method called “manipulateGamePiece calls the manipulator.manipulate() method.
8.	In your main method, create a robot object and a GamePieceManipulator object. Set the Robot object’s manipulator variable equal to your newly created GamePieceManipulator object. Then call your robot’s manipulateGamePiece method.
9.	Go into your three manipulator classes and create manipulate() methods in there. These methods should output something identifying what kind of manipulator they are, e.g. “now shooting boulder.”
10.	In your main method, create six new objects, one for each game piece manipulator type and one for each FRC robot game type. Assign the appropriate robot objects the appropriate manipulators.
11.	Call the manipulateGamePiece method for each of your robot objects. For reference, when this assignment is complete, you should have a grand total of eight objects in your main method – the six game-specific robots and manipulators, and the two general ones as well.

When your assignment is complete, the last four lines of your main method will look something like this:
		robot.manipulateGamePiece();
		recycleRushRobot.manipulateGamePiece();
		steamworksRobot.manipulateGamePiece();
		strongholdRobot.manipulateGamePiece();
You will have four lines of output, each of which is a message describing a type of manipulator. Note a couple things:
1.	We defined a “manipulate” method for Robot.java so all robots can “manipulate’, even if the output is generic.
2.	We overrode “manipulate” in our manipulator subclasses, so when we called .manipulate() in Robot.java, it was able to perform more specific functionality. (Polymorphism.)
3.	In Robot.java, we created a manipulateGamePiece() method, which we never overrode. Since we extended Robot.java with our robot classes, they already had access to the manipulateGamePiece() method, despite us never defining it in those classes.
