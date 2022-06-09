## Write a program in C that prints the first 50 Fibonacci numbers, starting with 1 and 2

To be able to answer this question, you need to understand what a [fibonacci number](https://en.wikipedia.org/wiki/Fibonacci_number) is and how to derive a fibonacci sequence.

A fibnonacci number is any number in a sequence which happens to be the sum of the two preceeding numbers.

This means that the number `n` in a sequence will be expressed as:
```
n = (n-1) + (n-2)
```

For instance, this question states the numbers (1, 2) we should use to start our fibonacci sequence. This means that our sequence will be something like
```
1
2
1 +2 = 3
3 + 2 = 5
5 + 3 = 8
8 + 5 = 13
```

This means that if we assign our first two numbers to variables `first` and `second` and declare another variable called `next`, we can go ahead to represent them as.
```C
int first = 1;
int second = 2;
int next = first + second;
```
In the above case, the `next` variable becomes `3`. As soon as we get that one, we need to find what the next one after `3` will be. 

Since we are interested in what is after `3`, we will need to reset our `first` and `second` variables. You will realize that to get the number after `3`, our first variable now becomes `2` and the second variable becomes `3`. This gives us:
```
first = 2;
second = 3;
next = first + second;
=> next = 2 + 3; 
=> next = 5;
```
The process will then repeated for the variable `first` to become `3` and `second` become `5`. The `next` variable becomes `8` which is `3 + 5`.

I bet you now know how this works. If you don't, kindly go over it again to understand the steps. We can then go ahead and implement this concept as a C program.

## Coding a C program that prints the first 50 numbers
Below is the code in C program that does exactly what we have discussed about.
```
#include <stdio.h>

/**
 * main - main block
 * Description: Print the first 50 fibonacci numbers, starting with 1 and 2.
 * Numbers must be coma and space separated.
 * Return: 0
 */

int main(void)
{
	int count = 3; /* this is so because the first 2 members have been given already. My loop will therefore begin from the 3rd one */
  
	long int first = 1, second = 2;
	long int next = first + second;

	printf("%lu, ", first);
    printf("%lu, ", second);
  
	while (count <= 50)
    {
        /* Let's check if we are at the end of the list, if we are close with a new line */
		if (count == 50)
		{
			printf("%lu \n", next);
	     }
         else  /* if we are not at the end of the list, add a comma after the number */
         { 
		   printf("%lu, ", next); 
         }
        
        /* Reset the variables to get the next number */
        first = second;
        second = next;

        /* after resetting the variables, you need to find the next number */
        next = first + second; 
	    count++;
	}

	return (0);
}
```  
The output of the above code is:
```
1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233, 377, 610, 987, 1597, 2584, 4181, 6765, 10946, 17711, 28657, 46368, 75025, 121393, 196418, 317811, 514229, 832040, 1346269, 2178309, 3524578, 5702887, 9227465, 14930352, 24157817, 39088169, 63245986, 102334155, 165580141, 267914296, 433494437, 701408733, 1134903170, 1836311903, 2971215073, 4807526976, 7778742049, 12586269025, 20365011074 
```
### Conclusion
I hope you enjoyed reading this and it made you understand how to solve a problem like this. I would like to hear back from you. Is there anything I missed, or explained wrongly, or something you want me to elaborate more on?

Share with me what you also think. Mind you, I am also learning and your feedback will be valuable to me.

Thanks for reading and I would love to connect personally with you. If you are on Twitter, then you can [send me a DM](https://twitter.com/ehoneahobed) and let's have a good chat.