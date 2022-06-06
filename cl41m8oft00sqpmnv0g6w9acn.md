## Write a C program that prints the alphabet in lowercase

We are still in the introductory lessons to C programming, and in this article, we are going to write a program that will print all the alphabets in lowercase.

This task will introduce us to a very important aspect of programming known as looping. There are different types of loops, and they help us design complex programs.

Also, the use of loops in programming has the following importance:

- Reduce repetition of codes
- Saves time and energy
- Gives your program the ability to think; execute, or stop the execution of a block of code.

Now let's get to work.

We want to print all the alphabets, so we have to figure out a way for our program to print them one after the other.

What's the possible way out? Think about something.

You definitely know that the alphabets are in a range from `a` to `z` in ascending order. 

Armed with that knowledge, we can write a program that will check and compare a given value to the range and keep adding on till we get to the end of the range.

There are two types of loops that we can use to solve this problem.

- For loop 
- While loop


## Solve the problem with a `while loop`
```C
#include <stdio.h>

int main(void)
{
    /* Declare a variable and initialize it with the first member of 
       the range [a - z] 
    */
       
	char alphabet = 'a';
    
     /* check to see if the current value of your variable is less than 
         or the same as the last member (z) of the given range. While 
         the value is less, go ahead and print the value 
      */
	
	while (alphabet <= 'z')
	{
	    // print the value of the variable 
		putchar(alphabet);
		
		// increment the variable (ie: a becomes b)
		alphabet++;
	}

	putchar('\n');
	return (0);
}
```
The output of the above code is:
```
abcdefghijklmnopqrstuvwxyz
```

## Solve the problem with a `for loop`
The logic behind the for loop isn't much different from that of the while loop. However, they have different syntax, so you just have to pay attention to how the loops are supposed to be written.

```C
#include <stdio.h>

int main(void)
{
    //declare a variable
    char alphabet;

    for (alphabet = 'a'; alphabet <= 'z' ; alphabet++)
	{
	    // print the value of the variable 
		putchar(alphabet);
		
	}

	putchar('\n');
	return (0);
}
```
The output of the above code is:
```
abcdefghijklmnopqrstuvwxyz
```

### Conclusion
I hope you enjoyed reading this and it made you understand how to solve a problem like this. I would like to hear back from you. Is there anything I missed, or explained wrongly, or something you want me to elaborate more on?

Share with me what you also think. Mind you, I am also learning and your feedback will be valuable to me.

Thanks for reading and I would love to connect personally with you. If you are on Twitter, then you can [send me a DM](https://twitter.com/ehoneahobed) and let's have a good chat.