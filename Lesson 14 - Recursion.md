Lesson 14 – Recursion
	In computer science, recursion is the idea of a method calling itself. In a simple case, this would create an infinite loop. For example if you just had a method:
public void doSomething() {
	doSomething();
}
The only thing this would do is run forever until you got a memory-related error. This is always something you have to watch out for when using recursion. However, if you’re a bit smarter than that, you can create ways for a recursive method to stop itself – for example, using an if statement. If some condition is true, it should call itself. If that condition is not true, it should no longer call itself. Eventually, the condition becomes true, and the method stops running. In fact, you’ve already used recursion in your programs – in our Power Up menu method runGameMenu, the method calls itself until the game is over. This is recursive but does not go forever, because eventually the game time elapses and the method only calls itself while there is game time remaining.
	Check out this video on a basic but neat application of recursion: https://www.youtube.com/watch?v=fpuWkZs51aM
	And here’s a text guide of the same concept – it even uses the same problem as an example: https://introcs.cs.princeton.edu/java/23recursion/ it also goes on to explain more advanced problems you can solve. 
	It’s important to remember the terms base case and reduction step. Both the video and the document talk about base case; I think only the text mentions reduction step. Simple concepts but you have to know the verbiage.
	Another important concept not covered by either of these resources is “the stack”. The stack is how Java manages the methods that need to be executed. You can think of it like a literal stack of cards if each method is a card. If your program is not doing anything, there are no cards in the stack. As soon as your main method starts, a card goes on the stack (is “pushed” to the stack), representing your main method. If your main method calls another method, a card goes on the stack for that method. If that method calls a third method, an additional card goes on the stack. Java will always work on computing the method at the top of the stack – in other words, the method most recently added to the stack. This is why you can call methods from other methods, and the calling method will not continue in the background until the more recent method finishes execution. Very useful, or your variables would all be changing at the same time! As soon as a method is completed, the method is removed, or “popped” from the stack. Eventually, the program will work itself all the way back to the main method, and when that is completed, the program will end.
	Recursion adds a lot of method calls to the stack. If you add too many, you can get a “StackOverflowError”, which means the stack is too big and Java can’t handle it. Usually this means you have infinite recursion, or at the very least you’re probably using recursion wrong. If you see it, you’ll know what it is.
	Note that the word “stack” also refers to a kind of data structure. They function similarly to “the stack”, but you manage what gets pushed and popped instead of Java. These are useful and we may talk about them later in the course but we aren’t right now. I just wanted to bring them up in case you run into documentation regarding them.
	Recursion often makes sense conceptually, but it takes some practice to write the code. So give these a shot and let me know if you have questions.
	Assignment
1.	Without using loops, create a program that outputs the factorial of an input N.
2.	Say there are N robots. Each robot has six wheels. Calculate the total number of wheels on all the robots recursively. (Yes, you could just return n * 6, but that does not count as a solution to this problem. Your program should also not contain any loops.)
3.	Now say you again have N robots. You could number each of them starting from 1, so 1-N. Every even-numbered robot has six wheels. Every odd-numbered robot as eight wheels. Again, without using loops or multiplication, calculate the total number of wheels.
4.	Say you have a triangle that is composed of rows blocks. The first row has a single block. The second row has two blocks. The third row has three blocks, etc. Recursively calculate the total number of blocks in the triangle for an input N.
5.	Now imagine instead of the rows increasing in the “triangle” one at a time, they double each row (it wouldn’t really be a triangle anymore.) Calculate the total number of blocks in such a shape with N rows.
6.	Solve these problems (your code must be submitted; solving on the site is not sufficient although you could use that to check your work if you want – running it in Eclipse should tell you whether or not it’s working.)
a.	http://codingbat.com/prob/p163932
b.	http://codingbat.com/prob/p101409
c.	http://codingbat.com/prob/p158888
d.	Strings! Parsing practice, hooray http://codingbat.com/prob/p184029
e.	http://codingbat.com/prob/p101372
f.	http://codingbat.com/prob/p170924
g.	http://codingbat.com/prob/p118230
