## Betty Styles For C Programming Explained

## What is Betty style and documentation in C programming?
As part of the Software Engineering program at ALX and Holberton School, we are taught to employ the Betty style of coding and Betty documentation when programming in C.

These are a set of guides crafted to ensure that the code we write is well written, documented, and presented in a way that anyone can easily understand.

Betty has therefore been developed as a code checker that checks whether a code written in the C language follows the Betty styles and documentation. 

This checker throws in an error any time, it finds part of the written code violating either the styles or documentation guides.

Here is a summary of what the Betty checker checks for.

### Betty Style of Coding Summary
To ensure that the checker does not flag your code with errors, pay attention to the following:

### Multiple Statements or Assignments
In C programming, each statement is ended with a semi-colon `;`. According to the Betty style of coding, no two statements should be put on the same line. Each statement should be on a single line.

Also, don't put multiple assignments on the same line.

Example of unacceptable code:
```
printf("I am checking for Betty style \n"); printf("Oops! Betty says I have some errors /n");
```

The above code will be flagged by the Betty checker. The correct version will be:
```
printf("I am checking for Betty style \n"); 
printf("Bravo! You passed my test. /n");
```

### Indentation
One important thing that the betty checker looks for is how you indent your code. It is very critical about indentations, and for that matter, you will need to pay very close attention to it.

The rules for indentation in the Betty Style are:

- Never use spaces (don't click your spacebar key) for indentation.
- Use the tab key for indentation.
- Indent every block of code you write.
- You also have to indent the nested blocks of code.

To be able to apply this style of indentation, you will need to understand what a block of code is in c programming.

#### What is a block of code in C programming?
In C programming, a block is created with the curly brackets `{ }`. Hence, anything within the curly bracket needs to be indented. An example is what we do with the `main` function.

```
int main(void)
{
     printf("Here is your block of code \n");
     printf("Can you see how I have been indented \n");
}
```
Any other thing will also be indented as such. But if you introduce a new block of code within this block of code then you would have to also indent that as well.

An example of a block of code that you can introduce include:

- An if statement
- A while loop
- A do while loop
- A for loop
Any of these when introduced into your program will have their block of code indented as well. An example is:

```
{
     printf("Here is your block of code \n");
     printf("Can you see how I have been indented \n");
     
     if (true)
     {
           printf("I passed Betty test \n");
     }
}
```
You may also have one or more blocks of code nested in one another. Like an if statement within a while loop. You will need to further indent any additional block that you create.

> The trick is, any time you type a new curly bracket `{}` in your code, the content of that curly bracket needs to be indented.

There is however an exception when it comes to using `switch` statements. In order to prevent, double indentation in a switch statement, Betty style allows you to put the case labels on the same line without indenting them.

An example is:
```
int main(void)
{
	int var;

	var = 0;
	switch (suffix)
	{
	case 'g':
		var = 30;
		break;
	case 'm':
		var = 20;
		break;
	case 'k':
		var = 10;
	default:
		break;
	}
	return (0);
}
```

### White spaces
Among all the things that will worry you when it comes to following Betty style of coding, white spaces pose the biggest headache.

`You have trailing whitespaces` is one of the common errors that you are likely to come across.

#### What are these trailing whitespaces and how do you avoid them
Trailing whitespaces means that you have some empty space after a given statement. Unfortunately, this isn't something that you will be able to see with your eyes.

These trailing whitespaces usually come when you click your spacebar key to move on to the next statement.

Hence, to avoid that try not to use the spacebar often in your code especially after you have ended a statement.

Click the `Enter key` anytime you end a statement to avoid trailing whitespaces.

Another way by which trailing white spaces may be created is when you want to bring a statement or part of it from one line to the previous line. 

You will realize that, because of the indentation, almost every word has some spaces prior to it. Hence, when you bring it back to a previous line, you may have some blank spaces between the previous code on that line and the new one.

## How to use braces `{ }` in your code
For all non-function statement blocks: `if`, `switch`, `for`, `while`, the curly brackets should start and end on the first and last line respectively.

```
if (condition)
{
      // Your code goes here
}
else if (another condition)
{
      // Your code goes here
}
else
{
      // Your code goes here
}
```
The rule also applies to functions as well
```
	int function(int x)
	{
		body of function
	}
```
There are some exceptions to pay attention to. For any of the non-function statement blocks: `if`, `switch`, `for`, `while`, do not use the curly bracket when it is followed by only one statement.

Example:
```
	if (condition)
		do_this();
	else
		do_that();
```
However, if any other branch of the conditional statement has multiple lines then you will have to use the curly brackets for all of them. Example:
```
	if (condition)
	{
		do_this();
		do_that();
	}
	else
	{
		otherwise();
	}
```


Also, the rules for the braces doesn't apply to the `do while` loop.
```
	do {
		body of the loop
	} while (condition);
```
### Placing spaces in your code
Most keywords in C language should be followed by a space with the exception of the following which look like functions: `sizeof`, `typeof`, `alignof`, and `__attribute__`.

You are supposed to add spaces after the following: `if`, `else if`, `switch`, `case`, `for`, `while`, `return`.
Examples:
<table>
<thead>
<th>Keyword</th>	
<th>Space After</th>	
<th>Example</th>
<tbody>

<tr>
<td>if</td>	
<td>Yes</td>	
<td>if (condition)</td></tr>

<tr>
<td>else if</td>
<td>Yes	</td>
<td>else if (condition)</td>
</tr>

<tr>
<td>for	</td>
<td>Yes	</td>
<td>for (i = 0; i < 10; ++i)</td>
</tr>

<tr>
<td>while	</td>
<td>Yes	</td>
<td>while (condition)</td>
</tr>

<tr>
<td>return	</td>
<td>Yes	</td>
<td>return (1);</td>
</tr>

<tr>
<td>sizeof	</td>
<td>No	</td>
<td>sizeof(struct file)</td>
</tr>

<tr>
<td>typeof	</td>
<td>No	</td>
<td>typeof(variable)</td>
</tr>

<tr>
<td>alignof	</td>
<td>No	</td>
<td>alignof(variable)</td>
</tr>

</tbody>
</table>

#### Do not add spaces around (inside) parenthesized expressions
Don't leave a space after a bracket before writing the content of the bracket. You shouldn't also leave a space before the ending closing bracket.

Bad Example:
```C
	s = sizeof( struct file );
```
Good Example

```C
	s = sizeof(struct file);
```

#### Add spaces around (each side of) binary and ternary operators
Any of the following operators should have a space before and after them.
```
	=  +  -  <  >  *  /  %  |  &  ^  <=  >=  ==  !=  ?  :
```

but no space after unary operators:
```
	&  *  +  -  ~  !  sizeof  typeof  alignof  __attribute__  defined ++ --
```

NB: There are a few more styles that I need to talk about. I will update this article when I get the time.