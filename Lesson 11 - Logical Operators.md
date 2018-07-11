Lesson 11 – Logical Operators and Short Circuiting

You’re familiar with conditional statements -ifs, switches, and the clauses of while loops.  For ifs and while loops in particular, they have a clause which evaluates to a boolean value, true or false. Up until this point we’ve been using fairly simple conditions. However, conditions can become more complex, and contain multiple conditions inside of one. For example, consider this pseudocode snippet:
	if (weekday != “Saturday” AND weekday != “Sunday”) {
		System.out.println(“It’s not the weekend!”);
}
	We have two separate conditions here; we’re checking if weekday is not Saturday, and independently checking if weekday is not Sunday. In order for the statement to be true, both conditions must be true. In this case we used AND and two not equal statements. Here’s a different way we could do this:
if (weekday == “Saturday” OR weekday == “Sunday”) {
		System.out.println(“It’s the weekend!”);
}
	We can check if weekend equals one thing OR another. With OR, as long as either of the conditions are true, the statement will return true.
	You can stick as many ANDs and ORs in a clause as you want, although if it’s more than two or three it can become very difficult to read and you might be better off creating a variable that represents some subset of the conditions, and then using that in your statement.
	In Java we represent the logical “and” operator with two ampersands: &&. We represent the logical “or” operator with two pipes: ||.
	There is an additional logical operator called “exclusive or”, or “xor”. Xor returns true when exactly one of the conditions is true. So in our weekend example above, if we used Xor instead of or, that would probably work OK, because it’s never going to be both Saturday and Sunday at the same time. But if it were, using Xor would return false, whereas using or would return true, because with or all of the conditions could be true – it will return true as long as any of them are. In Jave the character for a logical Xor is the tophat, ^.
Order of Operations
	Since you can combine multiple operations in one condition, order of operations comes into play. Java will evaluate logical statements left-to-right, but it will evaluate statements in parentheses before going to left to right. So you can nest operations in parentheses if you need to. For example:
Boolean example = x == 6 && !(y < 4);
Short Circuit Evaluation
	Consider the following conditional statement:
if (false && x == 38234 || y != 38748 ^ z / 42 >= 3252 && true && varName == 12)
	There’s a lot of junk going on there, but if you look at the beginning, the very first condition is “false &&…”. Obviously, false will never be true, and since there’s a logical and, the false will need to be true in order for the entire condition to be true. Since that can’t happen, nothing else in the statement matters – it will always return false. Java is smart enough to detect this, and will immediately stop evaluating the statement after it determines that false is, indeed, false. The statement will return false.
	Short-circuit evaluation is important because it saves computer resources, but it can also have side effects on your program that you need to be aware of. Imagine you have some method that returns a boolean value that you call as part of a condition. For example:
If (getIsItTheWeekend()) {
	System.out.println(“It’s the weekend!”);
}
In this example, we’re calling a method, “getIsItTheWeekend()”, which returns a boolean value, and therefore is legal to stick in our if statement. However, getIsItTheWeekend might have other consequences besides just returning a value. For example, maybe there is a class variable called “day”, and whenever getIsItTheWeekend() runs, it increments the day variable from one weekday to the next, and then checks if it’s the weekend. I’m not saying that would be a good design, just that it’s possible. If that is the case, then every time the if statement runs, it will increment the class’s day variable. However, in the following example, short circuit evaluation will happen, and getIsItTheWeekend() will never run, so the day variable would not be updated:
If (false && getIsItTheWeekend()) {
	System.out.println(“It’s the weekend!”);
}
Whether or not you would want the method to run even in cases where it doesn’t matter would depend on your program. It is possible to tell Java to ignore short-circuit evaluation – to do this, you can use a single ampersand or pipe instead of double like you would normally, so & for non-short-circuited AND evaluation, and | for non-short-circuited OR evaluation. As a general rule, you don’t want to use these – short-circuiting is good, and it’s often bad program design to create situations where you need a conditional in a method to run. But, you should know they exist. Perhaps the most important reason to know these exist is because it’s possible to have a typo in your code where you only type one of them instead of both, and you won’t get a syntax error. Be careful of this situation – get in the habit of using both, all the time, unless you have a very specific reason to avoid short-circuit evaluation.
