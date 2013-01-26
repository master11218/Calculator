```_____``````_````````````_```````_`````````````
``/`____|````|`|``````````|`|`````|`|````````````
`|`|`````__`_|`|`___`_```_|`|`__`_|`|_`___``_`__`
`|`|````/`_``|`|/`__|`|`|`|`|/`_``|`__/`_`\|`'__|
`|`|___|`(_|`|`|`(__|`|_|`|`|`(_|`|`||`(_)`|`|```
``\_____\__,_|_|\___|\__,_|_|\__,_|\__\___/|_|```
`````````````````````````````````````````````````
`````````````````````````````````````````````````


Kevin Jiang | CIS195 | Spring 2013

Since the input we are dealing with here is a string, rather than integers, the full expression being computed is provided right from the start. Had it been like a typical calculator, where you submit the first input, followed by the operand, and finally the second input, the order of operations would not be as important since there is only one operand in use at any given point in time. Granted, the situation would be a bit trickier when taking parenthesis into account.

Consequently, the most important factor when determining how the output will be computed lies with the order of operations. Since the input is a string in infix notation (where the order of operations is not arranged from left to right), my approach would be to first convert the infix notation into postfix notation, also known as reverse Polish notation (RPN). Here, every operator now follows all of its operands. This essentially would mimic a stack, where the order of operations would be straightforward and the operations would be carried out from left to right. Wikipedia gives an example:

The infix expression "5 + ((1 + 2) * 4) − 3" can be written down like this in RPN:

5 1 2 + 4 * + 3 -

The expression is evaluated left-to-right, with the inputs interpreted as shown in the following table (the Stack is the list of values the algorithm is "keeping track of" after the Operation given in the middle column has taken place):

Input	Operation	Stack	Comment
5	    Push value	 5	
1	    Push value	 1
					 5	
2	    Push value	 2
		    		 1
					 5	
+	    Add			 3
					 5	    Pop two values (1, 2) and push result (3)
4	    Push value	 4
					 3
					 5	
*	    Multiply	12
					 5	    Pop two values (3, 4) and push result (12)
+	    Add			17		Pop two values (5, 12) and push result (17)
3	    Push value	3
					17	
−	    Subtract	14		Pop two values (17, 3) and push result (14)
		Result	   (14)	

When a computation is finished, its result remains as the top (and only) value in the stack; in this case, 14.

In order to convert the infix notation to postfix notation, one could use a loop to run through the string, and then pick out each of the operands and operators in the correct order of operations (starting with parenthesis, multiplication, division, etc). These values could then be inserted into a new string, or possibly even a linked list and the operations would be carried out one by one, until the answer is given at the end (until the stack is fully popped).

To account for division by zero, an if-statement could be used to check if a zero ever follows a division sign. To clear the input, a button could be added to just delete the string. Including decimals shouldn’t be too big of an issue since the decimal is being entered in string format. To deal with negative numbers, a negative sign that comes directly before a number would represent a negative number and hence subtraction would be used first.

