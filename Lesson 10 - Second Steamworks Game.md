In this lesson we’ll very briefly cover two concepts that you’ll need for the assignment, and then dive into another tutorial. This is primarily a review lesson. You’ll re-implement the Steamworks simulator, but instead of being a “game” where the user specifies an action for a robot, it will be a 3v3 showdown where simulated robots automatically score gears and fuel. For reference, my finished project was about 300 lines of code altogether, of which maybe 100-150 was copied from the previous SteamworksGame class.
First, two quick concepts. You’ve seen the word “this” before, and it refers to whatever class you’re in. So for example you can reference a class variable or method by typing “this.whatever”, or “this.whatever()”. An additional use of the word this is when a class passes itself as a parameter to a method. For example, if you’re in a Robot class method and you want to pass the robot object to a static method that breaks robots, you could do something like “RobotBreaker.breakRobot(this);”. You’ll see this in the tutorial.
Additionally, now that we’re using inheritance/abstract classes/interfaces and polymorphism, occasionally we lose specificity when dealing with an object. By that, I mean we’re using an object of some class, but the program is treating it as a member of a superclass or interface. If the subclass has additional methods that the superclass or interface does not have, we lose access to those methods when the program is treating it as the superclass. But, if we’re certain about what kind of object we have, to can cast the object to a more specific class, and we get access to all our methods. Casting is done by typing the desired class name in parentheses before the object being operated on. In the following example, my “Robot” variable is of abstract type FrcRobot, which doesn’t have a “scoreFuel” method because FrcRobots for games other than Steamworks don’t score fuel. I cast it to SteamworksRobot to access my scoreFuel method. Casting is convenient, but if you do an illegal cast you will get an error, so only use it when necessary and when you’re certain the object you’re casting is of the type you’re casting it to.
	((SteamworksRobot) this.robot).scoreFuel(fuelScored);


Assignment
	This tutorial will cover abstract classes, inheritance, interfaces, class/object composition, arrays, static variables and methods, and of course general implementation work. I recommend pulling open your “SteamworksGame” class from lesson 5, because we’ll copy and modify a fair amount of code from that.

	This is more truly a simulator than our previous game. In this program, there is no user interactivity other than the menu options and running the next turn. However, we will do a much better job of simulating the game. Instead of each alliance having a single possible action each turn (or no actions), we’ll create two alliances of three robots each. Each robot will have a manipulator, and each turn, each robot will use its manipulator. We will use Math.random() to simulate success and failure for each action.

1.	Create a new project called “Steamworks3v3”. Create a class called “Steamworks3v3” that contains your main method.
2.	Create an interface called FrcPlayable. For now, give it three methods: public void runAutonomous(), public void runTeleop(), and public int getTeamNumber(). We won’t actually implement autonomous in this tutorial, but let’s include it anyway. In theory, this interface would include other methods as well such as runDisabled(), but teleop and autonomous is enough for now.
3.	Create an abstract class called FrcRobot, which implements FrcPlayable. Give FrcRobot two protected class fields: int teamNumber and GamePieceManipulator manipulator. The GamePieceManipulator class does not exist yet but we’ll create it. By creating this abstract class, we declare that all FrcRobots have a team number and a manipulator. (In theory some robots don’t have manipulators, but we’re not worried about that for this project.)

Note that we implemented FrcPlayable, which means that every FrcRobot object must implement the methods defined in FrcPlayable. However, Eclipse does not give us any errors saying that we have unimplemented methods. This is because FrcRobot is abstract. When a superclass is abstract, Java is content to let the subclasses that extend it implement the methods defined in an interface.
4.	Although we don’t need to implement the interface methods in our abstract class, let’s go ahead and implement getTeamNumber. All it needs to do is return the robot’s team number. No need to override this in all of our subclasses; let’s implement it once in the superclass and forget about it.
5.	Create an abstract class called GamePieceManipulator. Define a public abstract void method manipulate();. By creating this abstract class, we’re saying that all manipulator objects, regardless of type, have a manipulate method.
6.	Now let’s extend FrcRobot with a class specifically for Steamworks robots. Create a class SteamworksRobot that extends FrcRobot. Note that when we extend FrcRobot, Eclipse tells us that we need to implement unimplemented methods; these are the methods from the FrcPlayable interface. You can have Eclipse auto-implement these for now and we’ll revisit the teleop method later.
7.	As mentioned, our simulator is going to have two alliances of three alliances each. Keeping track of a bunch of robots and hoping we know which are on which alliance would be scary, so let’s create a class to represent an alliance. Create the class “SteamworksAlliance”.
8.	Last time we did this, our SteamworksGame class had a bunch of class variables to represent the score of the red and blue alliances, in terms of gears and fuel. Since we have a class to represent an alliance now, we can just put those variables inside the class. Then whenever we create a new alliance the variables will be replicated and we don’t have to manually track them. In SteamworksAlliance, create two private ints, “gears” and “fuel”.
9.	We also need our alliance to keep track of our robots. Create a private array of SteamworksRobot objects called “robots”. Don’t worry about initializing the array or setting its size yet.
10.	Extend GamePieceManipulator by creating two subclasses: GearPlacer and FuelShooter. You can auto-implement the manipulate method for now.
11.	Our class hierarchy is now complete, but we do still need a class to run the game. Create the class “SteamworksGame”.
12.	Give SteamworksGame two private SteamworksAlliance variables – redAlliance and blueAlliance. Additionally, if you pull open your old SteamworksGame class, you’ll see a bunch of constants that define how Steamworks works (e.g. FIRST_ROTOR_GEARS, FOURTH_ROTOR_BONUS, etc.) Copy these constants into your new class. Be careful not to copy the variables that we replaced by creating SteamworksAlliance objects. Also, we aren’t going to worry about tracking high score in this version, so you can leave that variable behind.
13.	Let’s finish piecing the classes together and revisit our SteamworksAlliance class. Right now it has a couple int fields and an uninitialized array of SteamworksRobots. Create a constructor method that takes three SteamworksRobot objects and initializes the array accordingly. The order of the robots in the array is not important.
14.	Back in SteamworksGame, create a constructor that takes two SteamworksAlliance variables and initializes the SteamworksAlliance class fields.
15.	Now in SteamworksRobot, create a constructor that takes an int teamNumber and a GamePieceManipulator manipulator, and initializes the class fields. (Remember that the class fields are defined in the parent class, FrcRobot.)
16.	We said we’re going to simulate success and failure of the manipulators using Math.random. Let’s set this up by adding a private double called “successProbability” to both the GearPlacer and FuelShooter classes. (For FuelShooter it should be called “successProbabilityPerFuel”.)
17.	FuelShooter will also need an int field for “fuelShotPerAttempt”, as robots will shoot more than one fuel at a time.
18.	Now create constructors for GearPlacer and FuelShooter that accept parameters for, and then initialize, their class fields – so two variables for FuelShooter, and one for GearPlacer.
19.	We’ll have more changes and implementation work to do on our classes, but it’s time to start making objects. In order to do this we’ll have to piece some methods together. Go to your main method and paste the following:

public static void main(String[] args) {
		runSteamworks3v3Simulator();
	}

20.	Paste the following runSteamworks3v3Simulator() method into your Steamworks3v3 class:

	private static void runSteamworks3v3Simulator() {
		SteamworksAlliance redAlliance = createRedAlliance();
		SteamworksAlliance blueAlliance = createBlueAlliance();
		SteamworksGame simulator = new SteamworksGame(redAlliance, blueAlliance);
		simulator.runMainMenu();
	}



21.	Paste the following methods into SteamworksGame:

public void exitProgram() {
		displayExitMessage();
	}
	
	public void displayWelcomeMessage() {
		System.out.println("Welcome to the Steamworks Simulator.");
	}
	
	public void displayMainMenu() {
		System.out.println("Enter a number to perform an action.");
		System.out.println("1: New game of Steamworks");
		System.out.println("2: Exit program.");
	}
	
	public void displayGameMenu() {
		System.out.println("1: Run next turn");
		System.out.println("2: Skip to end of game");
	}

	public void displayExitMessage() {
		System.out.println("Thanks for playing Steamworks!");	
}
22.	Copy your “runMainMenu” method over from your old SteamworksGame class. But now it should only have two menu options: 1-startNewGame(). 2-exitProgram(). Keep the default case.
23.	To fix the syntax error for no method found for “startNewGame()”, create a public void method startNewGame(). You don’t want to copy this one over from your old SteamworksGame file because this method will work differently. You can leave it blank for now.
24.	If you save all your work, the only place you should have outstanding syntax errors right now is in Steamworks3v3, on the method calls “createRedAlliance” and “createBlueAlliance”. These methods are where we are going to create our SteamworksRobot and SteamworksAlliance objects. Go ahead and create methods with these names in your Steamworks3v3 class. They should be private and return SteamworksAlliance objects. We will implement these methods for real in step 26; for now they can just return null – but the method signature has to be correct.
25.	You’ll notice that even after you create the methods, you still have syntax errors – “Cannot make a static reference…”. This is because the main method is static, and this is being called from the main method (by way of the runSteamworks3v3Simulator method.) We never create an instance of the Steamworks3v3 class, hence it being static. Simply make these two methods static to fix the error.
26.	Now it’s time to implement the methods that create alliances. You will want to use the constructor we defined for SteamworksAlliance that takes three SteamworksRobot objects as parameters. So we will need to create three such objects for each alliance. And to create a SteamworksRobot object, you’ll want to use the constructor we defined that takes a team number and a GamePieceManipulator object, so you’ll need to create a GamePieceManipulator for each robot. Use the appropriate constructor depending on which kind of manipulator you’re making. The probability of success for each action should be a number between 0 and 1, where 1 would be 100% successful. Implement the createRedAlliance and createBlueAlliance methods. Each alliance should have two robots that have GearPlacer manipulators, and one robot that has a FuelShooter manipulator.
27.	It would be nice if we could run our program, but right now the game ends immediately after starting because the SteamworksGame.startNewGame method does nothing. Implement this method. You can look off your old startNewGame method, but consider that resetting each alliance’s score is different than it was before. Create and implement a resetScore() method in SteamworksAlliance to reduce code duplication. Then your startNewGame method can call that method, along with any other actions it must perform. The last thing startNewGame needs to do is call runGameMenu() to get us into a game. You’ll implement runGameMenu() next step.
28.	Implement runGameMenu. I suggest looking off your previous SteamworksGame implementation, but now the only actions on the menu should be “runTurn()” and “skipToEnd()”. Again, leave the default case. Protip: you can copy the entire skipToEnd() method from your old code. You will also want to copy over displayGameStatus(), though we will need to change this method later on. For now you can comment out any lines of your old displayGameStatus() that give syntax errors.
Now we need to implement runTurn(). Create the method; private void. Again, let’s split up the method into small chunks. Here’s my entire runTurn() method:

	private void runTurn() {
		redAlliance.runTeleop();
		blueAlliance.runTeleop();
}

29.	Define a “runTeleop” method in your SteamworksAlliance class. To implement this method, consider what it has to do. There are three robots on the alliance, and each of them is going to do something each turn. We have an interface, FrcPlayable, that mandates that each robot object as a “runTeleop” method. So really, the alliance-level runTeleop method simply has to call the robot-level runTeleop method for each robot on the alliance. Implement this method.
30.	If we were to make a more complete simulator, a robot would do lots of things in teleop – drive, light up, crash, etc. But for now, all it can do is run its manipulator. And since we have used an abstract class for our GamePieceManipulators, every manipulator can be accessed the same way. So the SteamworksRobot.runTeleop method can literally be one line: manipulator.manipulate(). Implement this method.
31.	Calling .manipulate in SteamworksRobot.runTeleop will call the manipulate method that belongs to whatever subclass of GamePieceManipulator the given SteamworksRobot object happens to have. So it could call GearPlacer.manipulate or FuelShooter.manipulate. We need to implement both of these methods. In both methods, add a SOP that announces what the robot is doing. For example, here’s the first line of my GearPlacer method (I have a robot class field; you will implement this in a couple steps):
System.out.print("Team " + this.robot.getTeamNumber() + " approaches the peg...");
This will both make it easier to follow what’s going on in your program when you run it, and makes your simulator more interesting.
a.	In GearPlacer.manipulate, use Math.random to get a random number between 0 and 1. If the manipulator’s probability of success is greater than that number, SOP that the robot has scored. Otherwise output that they dropped the gear.
b.	In FuelShooter.manipulate, the robot is going to shoot some number of fuel, based on the “fuelShotPerAttempt” variable. Using a new random number for each shot, calculate the total number of successful shots, and SOP that number.
32.	You can now run your simulator, and you’ll see output of each robot attempting actions, along with whether or not they succeed. However, we’re only outputting their results, not keeping track and scoring it. Right now, the determination of whether or not a robot scores is in the manipulate() method of a GamePieceManipulator object, but the variables for scorekeeping is all the way up at the SteamworksAlliance. We don’t have a way to access the SteamworksAlliance variable from inside the manipulator – so let’s change that. We’ll need to create a way to link from the manipulator to the alliance. In our hierarchy, we go SteamworksGame - > SteamworksAlliance -> SteamworksRobot -> GamePieceManipulator. It’s easy to go “downstream” in the chain, since each link belongs to the class above it. But if we want to go “upstream”, we will need to pass each object to the objects it owns. For example, SteamworksAlliance needs to pass itself to SteamworksRobot, and SteamworksRobot needs to pass itself to GamePieceManipulator.
33.	Go into your GamePieceManipulator class and add a protected FrcRobot field called robot. This defines that all manipulators will have a robot variable, so we’ll be able to pass an FrcRobot to them. Additionally, define and implement a setter method for the robot variable.
34.	Go into your SteamworksRobot class and create a field for a SteamworksAlliance. Implement a setter method.
35.	Now we have variables for the information we need; we just need to pass it along. The easiest place to do this is in object constructors, because then it will happen automatically when objects get created. Go into SteamworksAlliance and add a line to your constructor: this.setRobotsAlliance();.
36.	Implement the SteamworksAlliance.setRobotsAlliance method. The method needs to set the alliance variable of every robot on the alliance. To do this, you will need to use the this keyword to pass the SteamworksAlliance object to the robot.
37.	Now we need to do the same thing for passing the robot to its manipulator. Inside of SteamworksRobot, in the constructor, add a line for “this.setManipulatorRobot();”. Define and implement setManipulatorRobot. Note: you could define setManipulatorRobot inside of SteamworksRobot, but it is better to do it in FrcRobot. When using abstract classes, you need to consider, for each method, whether that method is common to the parent class, or specific to a subclass. Setting a robot manipulator’s robot object is not a Steamworks-specific action, so it should go in the FrcRobot class.
38.	Since we put these method calls in the constructors, they happen automatically when objects get created so we don’t have to worry about doing it manually. Now we’ve created the data link between a manipulator and a SteamworksAlliance, so we can go back into our manipulate() methods and make the scoring work. You already have SOPs; that is fine, those can stay. But in addition to SOPs, when the robot successfully scores gear or fuel, add a method call. You should define and implement the following two methods inside both your SteamworksRobot and SteamworksAlliance classes. The method in SteamworksRobot doesn’t need to do anything other than call the method in SteamworksAlliance – it’s simply acting as a pass-through. In SteamworksAlliance, the methods must update class variables as appropriate.
a.	protected void scoreGear();
b.	protected void scoreFuel(int fuelScored);
39.	Now the game is running and the last thing we need to do is revisit our displayGameStatus() method to update the scoreboard after each turn. This time the scoreboard should show four things. Implement a-c below.
a.	Each alliance’s gears
b.	Each alliance’s fuel
c.	The seconds remaining
d.	Each alliance’s total score. See the next step for this one. 
40.	To calculate each alliance’s score, we’ll need to bring over logic from the old SteamworksGame. Copy and paste your calculateRotorScore and calculateFuelScore methods.
41.	Last time, we had a method for calculating red’s score and one for calculating blue’s. This time that is not necessary because we have a class for a SteamworksAlliance, and SteamworksAlliance objects which we can pass around. Create a static method in SteamworksGame that takes a SteamworksAlliance parameter and calculates the score for that alliance. Return the total score as an integer.
42.	Now that we have a method that calculates the scores, plug the scores into the scoreboard.
43.	Run your simulation. You’re done! Congratulations.
