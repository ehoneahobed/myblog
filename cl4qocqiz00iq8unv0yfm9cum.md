## What will this Recursive function in C Print and what is the logic behind it?

```C
#include <stdio.h>

int display(int x)
{
    if (x < 0) 
    {
        return (0);
    }
    printf("%d", x + display(x - 1));
    x--;
    return (x);
}

int main(void)
{
    display(4);
    return (0);
}
``` 
To be able to find what the above program will print, you need to understand recursion and how recursive functions work. 

The simplest way will be to run the code in a compiler, but being able to deduce it based on the logic of the program is what the question seeks.

I am going to go on and explain the logic behind the code, presuming that you know about recursion and recursive functions. If you have no idea about them, then try and read on them before.

Since the question is looking for the output, we have to be interested in any line of code that prints out something to the screen.

In the code above, you can see that there is only one line that prints out something to the screen and that line is:
```C
printf("%d", x + display(x - 1));
```

However, the print line even though within the `display()` function also calls another `display()` function which makes the function a recursive function.

The presence of the recursion of the function also draws our attention to the return value for the function. This is because, the return value is what will be provided anywhere the function is called.

This means that we need to figure out both what is printed out and what is returned in order to get the right output for the whole code.

Let's therefore take them one by one.

## What does this function do and what does it return

```C
int display(int x)
{
    if (x < 0) 
    {
        return (0);
    }
    printf("%d", x + display(x - 1));
    x--;
    return (x);
}
``` 
The first line of the body of the function checks to see if the variable (`x`) passed to it is less than zero and returns zero if that is true.

The function then goes on to print the sum of the variable plus the return value of the `display()` function when the argument for the function is `x-1`.

In the next line, there is a decrement on the variable `x` before returning the current value of `x`. The decrement on `x` means that, we will subtract one from `x` and return the resulting value.

This means that every time, the `display()` function is called, it returns one less than the number that was passed to it as an argument. An example will be if we call `display(2)`, then it is going to return `2-1` which be `1`.

Since the question gave `display(4)`, it means we need to have the return values for 4, then the `printf` statement in there will also require the return value for 3 which in turn will require return values for 2, etc.

We will have to keep reducing the numbers till we get to zero. So, let's have a table with the numbers and their return values:

<table>
<thead>
 <th><td>Display function argument</td><td>Return value</td></th>
</thead>
<tbody>
<tr><td>4</td><td>3</td></tr>
<tr><td>3</td><td>2</td></tr>
<tr><td>2</td><td>1</td></tr>
<tr><td>1</td><td>0</td></tr>
<tr><td>0</td><td>-1</td></tr>
<tr><td>-1</td><td>0</td></tr>
</tbody>
</table>

Now that we know what the function does and the values it returns at each stage, we can go ahead look at what the function prints at each stage.

## What does the function print at each stage?

```C
printf("%d", x + display(x - 1));
``` 
At each stage, the function prints the sum of the argument `(x)` passed to the function and the return value of the `display()` function with argument of one less than the initial argument `(x-1)`.

Since we know that, the function in the question above runs multiple times with values starting from `4` down to `0`, we have to find the value that will be printed with each value.

Let's use a table to illustrate that.

<table>
<thead>
 <th><td>Display function argument</td><td>What to print value</td><td>Argument + Return value</td><td>Value printed</td></th>
</thead>
<tbody>
<tr><td>4</td><td>4 + return value for display(3) </td><td>4 + 2</td><td>6</td></tr>
<tr><td>3</td><td>3 + return value for display(2)</td><td>3 + 1 </td><td>4</td></tr>
<tr><td>2</td><td>2 + return value for display(1)</td><td>2 + 0</td><td>2</td></tr>
<tr><td>1</td><td>1 + return value for display(0)</td><td>1 + -1</td><td>0</td></tr>
<tr><td>0</td><td>0 + return value for (-1)</td><td>0 + 0</td><td>0</td></tr>
</tbody>
</table>

Because of the recursion, the code will print that of `display(0)` first followed by `display(1)` then continuously till the last one (`display(4)` in this case) is printed.

As such, you have the final output being: 

```C
00246
``` 

### Conclusion
I hope I was able to simplify this enough but if you have questions on any of the things I explained above or have some suggestions, you can comment it down below or hit me up on [Twitter via a DM](https://twitter.com/ehoneahobed) and let's chat it out.

Thanks for reading.
