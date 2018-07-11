This lesson is more review, but I’m going to be enforcing code styling more strictly so that’s an additional thing you’ll need to pay attention to. We’re going to continue with the Steamworks game you started last lesson. Note that the code you submitted for that project may not fit the style guidelines outlined below, even if I accepted it. So you’ll have to go back and check that.
From here on out I will not evaluate programs that have sloppy code styling. I will send it back and tell you to fix styling and resubmit. I’m not saying I’ll bounce it if it’s not perfect, but it needs to be pretty close. Style rules apply even to code you copy and paste from sources I give you, into your program. 
	Starting immediately I’ll be looking at the following items. This list will grow over time:
-	Indentation
-	Variable names need to be relevant and reasonable
-	No excessive whitespace
-	Items must be cased properly – camelCase for variables, TitleCase for classes, and UPPER_CASE for constants.
-	If I specify a name for a class/variable/method/etc, you must use that exact name.


Ok, so back to the project. You left off with two classes, one that has your main method and kicks off the start() method of SteamworksGame, and SteamworksGame, where everything is actually going to happen. Note how little code is in the main method in this program – this is generally a good practice. (There are always exceptions – just something to consider.) Last week you did steps 1-8 so we’ll pick up with step 9.

9.	We have a start method and we have a few menu methods. In order to make it easier to run and test our code, let’s get our menu working so we can trigger other methods that we write. Of course, getting our menu working isn’t the only way we could accomplish this goal, but it will work. We’ll code up our menu, and then make it so that the menu options work properly. Paste the following method into your SteamworksGame class:
	public void runMainMenu() {
		displayMainMenu();
		
		Scanner inputReader = new Scanner(System.in);
		int userSelection = inputReader.nextInt();
		
		switch (userSelection) {
			case 1:
				startNewGame();
				break;
			case 2:
				displayHighScore();
				break;
			case 3:
				exitProgram();
				break;
			default:
				runMainMenu();
break;
		}
	}
	This will result in some syntax errors because these methods don’t exist yet. If you want, you can mouse over the squiggly lines and choose the “create … method” option. Be careful; sometimes there is a second option called “change to…” which will change your method call to a method that already exists. This will get rid of the error, but it won’t do what you want it to do because now you’re calling a different method. And since the red squiggly is gone, it will be harder for you to notice it. So make sure you click “create” instead of “change to”, if there is more than one option. The create option will create what is known as a method “stub” for you, but won’t fill in any of the code.

	Also note we’re using a “switch” statement here. Codecademy covers these but we haven’t discussed them during this course, but it’s basically just an if-elseif-else statement with different syntax. The “default” case is the “else” clause, and the “case” values are the if/else ifs. Notice that the default case calls runMainMenu – this means that if the user enters something that is not an option, it will just call itself again to let the user try again. A method calling itself is called recursion, which we will learn about later in the course. For now don’t worry too much about it, but keep in mind it’s dangerous – if a method calls itself without a way to stop calling itself, it will create an infinite loop. Here, it will stop calling itself as soon as the user enters a valid option.

10.	Let’s tackle the easy stuff first – implement the exitProgram() method. All this method needs to do is call the “displayExitMessage()” method that already exists. After that, the program will end, because runMainMenu is not in any kind of loop. We’re not actively terminating the program, it just finishes on its own.

11.	Now let’s tackle “displayHighScore()”. We don’t currently store the high score, but it won’t be too hard to do, and since the displayHighScore method doesn’t have to calculate the high score, only display it, this method will be easy to write.

a.	Add a class variable, integer, to SteamworksGame. Call it “highScore”. Give it a default value of zero, so it can be displayed even before the user plays a game.
b.	Now write your displayHighScore method. It doesn’t need to return anything, and all it needs to do is output the high score with a short message.
c.	Ok I lied – it has to do one more thing. If all it did was display the high score, the program would terminate after it does so, same as if the user had chosen to exit the program. Again, since there’s no loop in “runMainMenu”, once the user selects an option, that option will execute and then runMainMenu is over. So at the end of displayHighScore, we need to call runMainMenu again. This way, after a menu option is chosen and executes, it runs the menu again so the user can select another choice.

12.	Now that the easy stuff is out of the way, we need to make the actual game. Create your startNewGame method if you haven’t already. This method does not need to return anything or take any parameters.

13.	Every time a user starts a new game, we need to update our class variables that represent game state. In other words, we need to set all of our class variables to values they will be at the beginning of a game of Steamworks. Our constants, of course, do not change. We have one other variable that does not change when a new game is started – do you know which one? So one variable does not change, five do. Set the five variables that need to change to the values that they should be at the beginning of a game of Steamworks. (Hint: some should be zero, but not all – we’re assuming the pilots score the free gear!)

14.	After our variables are set, we’re going to need to run our game menu to let the user start playing. Add the following method call to the end of your startNewGame method: runGameMenu();

15.	We’re calling runGameMenu, but it still needs to be defined. Create this method. It does not return anything, and doesn’t need any parameters.
a.	This method will look similar to runMainMenu but it’s a bit more complicated. First, this should be in a loop – we don’t want it to run forever, we want it to run for some specific amount of time…specifically, until the game is over. We’re using seconds to measure when the game is over. So create a loop that will run until the game is over. I suggest using a while loop for this for reasons that will become clear later on. Basically, instead of running a set number of times, run until the number of elapsed seconds is greater to or equal than the game’s duration.
b.	First thing inside the loop, call the method “displayGameMenu()”, which I provided for you last week.
c.	Each time this method runs, we’ll need to get user input since we’re running a menu. Create a scanner object that gets an integer from the user, just like we did for the main menu.
d.	Create a switch statement that properly handles whatever the user inputs. You can again look at runMainMenu for how to set up a switch statement. You can look at the “displayGameMenu()” method to see what options the user will be inputting.
e.	Each branch of the switch statement should call a method to do what the user said, e.g. place a gear for red, score ten fuel for blue, etc. Create methods for each of these actions. They can be empty for now; you just need something so the method exists. None of them need parameters or return anything. Once you’ve created the method stubs, update your switch statement to call those methods when the correct branch of the switch statement is hit. To be clear, your switch statement should have six cases – 1 through 6 – that each call a method. Also add a default case that calls displayGameMenu(). This is the same idea as with the main menu; if the user enters something wrong, just run the menu again so they can retry.
f.	At the end of your loop, make sure to update the number of seconds that have elapsed. Increment it by five.

16.	Once you implement all of the methods you just defined, you’ll have a working game. Because you created a loop that runs until the game seconds have elapsed, and increments the game seconds, you’ve just created a turn-based system. Now we just need to make the methods that you just defined do something. But before we do that, let’s add one more thing to runGameMenu. Since this method is a loop and will run an entire game, we know that when this method finishes, the game is over. When the game is over, let’s send the user back to the main menu so they can start another game, view the high score, or quit. To bring up the main menu, simply re-use your method call – add “runMainMenu();” as the very last line of your runGameMenu method, just before the closing bracket.

17.	You now have six different methods that you need to implement – placing gears, scoring fuel, etc. We have variables for all the things these methods do, so you just need to appropriately update those variables inside the methods. Implement these methods. Hint: each of these methods is literally one line long. Except for conserve battery power, that one’s zero!! Second hint: “skipping to the end of the game” means setting the time equivalent to what it would be at the end of the game.

18.	Now your turn actions are implemented and so is your menu, so you can actually start playing your game. However you’ll probably notice that it’s not very fun, because you can’t see the results of any of your actions. Nothing outputs the score. Since Steamworks was renowned for the accuracy of its high goal boilers*, let’s add “real time scoring”. Every time the game menu is shown, let’s output the status. We don’t want the status to interfere with the menu, so let’s output the status before the menu. In your runGameMenu method, on the line immediately before “displayGameMenu();”, add a method call for “displayGameStatus();”.

* If the scoreboard always reads zero, but no one ever scores any fuel, it’s always accurate. #SteamworksStrategies

19.	Now implement the displayGameStatus method. This may actually be the trickiest part of the project, so let’s break it up:
a.	The scoreboard should show the score for each alliance, also how many gears they’ve each scored, and how many seconds remain. How many gears each has scored and the time remaining is easy because we have variables for those. (Make sure you don’t confuse how many seconds have passed with how many remain.) However, the actual score is tougher. Since displayGameStatus is going to have to handle logic for displaying the score, let’s put the logic for calculating the score somewhere else. Start by declaring two variables, integers, for redScore and blueScore, and set their value equal to the output of two new methods, calculateRedScore() and calculateBlueScore(). Neither of these new methods need any parameters.
b.	Go ahead and stub out those two methods. Remember that these do need to return something; they should not be void. Don’t worry about implementing them just yet; we’ll do that in a sec.
c.	Back in your displayGameStatus method, you won’t have syntax errors anymore because the methods you’re using now exist. Declare another variable for secondsRemaining and calculate that value, then write three SOPs to output the gears for each alliance, the score, and the seconds remaining. Now displayGameStatus is actually done – it just won’t work right until we implement calculateRedScore and calculateBlueScore.
d.	Calculating red and blue score will be almost identical. Let’s start with calculateRedScore. Logically, an alliance’s score is pretty simple since we’re not worrying about autonomous, penalties, etc. It’s just their fuel points plus their gear points. I like splitting things up into small tasks, so here’s my calculateRedScore method. You can actually just copy this if you want:

	private int calculateRedScore() {
		int rotorsScore = calculateRotorScore(redAllianceGears);
		int fuelScore = calculateFuelScore(redAllianceFuel);
		
		int totalScore = rotorsScore + fuelScore;
		
		return totalScore;
}
e.	Implement calculateBlueScore the same was red score was done, but obviously using different variables. Consider how similar the code is for these methods. This is an opportunity to improve our program – if we did things a bit differently, there could be a single method called “calculateAllianceScores” that takes a variable for which alliance to calculate scores for. Perhaps making that change will be a future project.
f.	Though we have some duplication in the “calculate…” methods, we’re able to re-use the methods they use – “calculateRotorScore” and “calculateFuelScore”. It’s time to define those methods. Note that these methods each take an integer parameter – they do not look at the class variables, since they don’t know which color they are operating on.
i.	Calculating fuel score is easier so let’s do that first. You have a constant for how many fuel must be scored for a point, and you have a variable for how many fuel have been scored. Simply do some division and you have the base kPa. Bonus: when you divide two integers in Java, it always rounds down. That can be annoying sometimes, but in this case it matches the logic of Steamworks, so you literally just have to divide.
ii.	Make sure to implement a bonus for if they get at least 40 kPa. In the end, you’re just going to return an integer with their total fuel points, regardless of whether or not bonus points have been added to it.
iii.	Now gears – this is a bit trickier. There are a couple ways you could do it. For simplicity’s sake I recommend just using a few if statements. I did it with four of them. Hint: one if statement, if true, has a greater effect than simply adding an additional forty points.
iv.	When you’re done, your methods will return a fuel score and a rotor score, which your calculateRed/BlueScore methods are already using. In turn, displayGameStatus will start working because the calculateScore mehods are working. This also means your displayGameStatus method works. Cool!

20.	We’re very close to done now – in fact, you could play the game as is. Try it out! However, the one thing that is not working is the “show high score” function. You already implemented the method to output it, but your program needs to keep track of what it is. The easiest way to do this is at the end of each game, check if either alliance scored higher than the high score (which you’re storing as a class variable), and if they did, update the high score variable with the new score. The code that runs when a game ends is at the bottom of your runGameMenu method – remember, we added a line to “runMainMenu()” as the very last line. So, before “runMainMenu()”, add a few lines that compare the current scores to the high score. Protip: it sure would be handy if we’d implemented methods to calculate red and blue scores for us to use here!!

21.	After you’ve implemented the high score tracker, you’re done! Have fun. Or not, it gets boring after about the first play. But please run through it a few times to test various things. Can both alliances score as you expect them to? What happens if you choose to end the game early? What if you don’t end the game early, does it correctly end at the proper time? Can you restart after it ends, or does something unexpected happen? Etc. Run through it a few times before you submit, please.
