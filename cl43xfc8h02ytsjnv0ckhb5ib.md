## Write a program that prints all possible combinations of single-digit numbers

```
0, 1, 2, 3, 4, 5, 6, 7, 8, 9
```
The question is about writing a C program that produces the outcome above.

There are several ways we can have a program to print all the possible combinations of single-digit numbers. In this tutorial, we will look at how to use:
- `putchar`
- `printf`

Also, for each of them, we can look at multiple ways of achieving the expected outcome. In this tutorial we will take a look at how to use two different types of loops to achieve the result;

- For loop
- While loop


## Using `putchar` to print all combinations of single-digit numbers
First we will look at how to do that with a `for` loop and afterwards implement the same code using a `while` loop.

By default, the `putchar` function is used for displaying single characters to the screen, but we need to make it print integers this time round.

What can help us here is the fact that the `putchar` function recognizes ASCII codes and is able to print the corresponding integer value of any ASCII code. This means we would also need to know the ASCII codes for the digits (0, 1, 2...9).

<table>
<thead>
<th>ASCII Code</th>
<th>Interger Value</th>
</thead>
<tbody>
<tr><td>048</td><td>0</td></tr>
<tr><td>049</td><td>1</td></tr>
<tr><td>050</td><td>2</td></tr>
<tr><td>051</td><td>3</td></tr>
<tr><td>052</td><td>4</td></tr>
<tr><td>053</td><td>5</td></tr>
<tr><td>054</td><td>6</td></tr>
<tr><td>055</td><td>7</td></tr>
<tr><td>056</td><td>8</td></tr>
<tr><td>057</td><td>9</td></tr>
</tbody>
<table>

#### With a `for` loop

```
#include <stdio.h>

/**
 * main - main block
 * Description: Print all possible combinations of single-digit numbers.
 * Numbers must be separated by commas and a space.
 * You can only use `putchar` to print to the console.
 * You can only use `putchar` up to four times.
 * You are not allowed to use any variable of type `char`.
 * Return: 0
 */

int main(void)
{
	int x;

	for (x = 48; x < 58; x++)
	{
		putchar(x);
		if (x < 57)
		{
			putchar(44);
			putchar(32);
		}
	}
	putchar('\n');
	return (0);
}
```

If you don't know the ASCII codes and would still want to use the `putchar`  function, there is a way around it. 

You can forcefully convert an integer to a character inside the `putchar` function. This can be done by add `'0'` to the integer.

The above code can therefore be re-written as:
```
#include <stdio.h>

int main(void)
{
	int x;

	for (x = 0; x < 10; x++)
	{
	    putchar(x + '0');
		if (x < 9)
		{
			putchar(',');
			putchar(' ');
		}
	}
	putchar('\n');
	return (0);
}
```

 

#### With a `while` loop
Let's use the `while` loop to answer the tasks in the same way we did for the `for` loop.

- Using the ASCII codes

```
#include <stdio.h>

int main(void)
{
	int x = 48;

	while (x < 58)
	{
		putchar(x);
		if (x < 57)
		{
			putchar(44);
			putchar(32);
		}
		x++;
	}
	putchar('\n');

	return (0);
}
```


- Converting integers to characters with the `putchar`

```
#include <stdio.h>

int main(void)
{
	int x = 0;

	while (x < 10)
	{
		putchar(x + '0');
		if (x < 9)
		{
			putchar(',');
			putchar(' ');
		}
		x++;
	}
	putchar('\n');

	return (0);
}
```

## Using `printf` to print all combinations of single-digit numbers

- With a while loop

```
#include <stdio.h>

int main(void)
{
    int x = 0;

    while (x < 10)
    {
        printf("%d", x);
        if (x < 9)
        {
            printf(", ");
        }
        x++;
    }
    printf("\n");

    return (0);
}
```

- With a for loop

```
#include <stdio.h>

int main(void)
{
    int x;

    for (x = 0; x < 10; x++)
    {
        printf("%d", x);
        if (x < 9)
        {
            printf(", ");
        }
    }
    printf("\n");

    return (0);
}
```

The outcome for all the above codes are:
```
0, 1, 2, 3, 4, 5, 6, 7, 8, 9
```