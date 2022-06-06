## Bash Script That Prints A Number With Two Decimal Places

Another task that I had to tackle as part of the lessons on shell expansion in my ongoing ALX Software Engineering course was to write a bash script that prints a number with two decimal places.

Let's take a practical example and solve it to explain how to print a number with two decimal places.

Practical Example:
```
Write a script that prints a number with two decimal places, followed by a new line.
The number will be stored in the environment variable MYNUM
```

Up until this point, we had always relied on the `echo` command to display or print somethings to the screen. As such, upon reading this question, my intuition defaulted to using the `echo` command to perform the task.

Unfortunately, I learned too soon that the `echo` command prints out only whole numbers and doesn't print floats by default. This means that we need to rely on something else to help us print floats or decimal numbers to the screen.

The `printf` command is the saviour of the situation. This is a popular command in programming languages like C but the bash shell equally utilizes it for the same purpose.

`Printf` is able to let us determine the format of the output we want. Hence, in this case the `printf` command will help us to format the output to be in 2 decimal places.

## How to format output with the `printf` command
Let's look at the normal synthax of the `printf` command.
```
printf options arguments
``` 
It may also be presented as
```
printf options [format specifiers] arguments
``` 
The format specifiers are what tells the `printf` command what the format of the output should be. They also point to the arguments and restricts the type or format of values the `printf` command takes in as arguments. 

Examples of format specifiers that you are likely to use include
<table>
<thead>
<th>Format specifier</th>
<th>Description</th>
</thead>

<tr>
<td>%d</td>
<td>decimal (integer) number (base 10)</td>
</tr>

<tr>
<td>%f</td>
<td>floating-point number</td>
</tr>

<tr>
<td>%i</td>
<td>integer number (base 10)</td>
</tr>

<tr>
<td>%o</td>
<td>octal number (base 8)</td>
</tr>

<tr>
<td>%x</td>
<td>hexadecimal number (base 16)</td>
</tr>

<table>

Let's see the `printf` in action so we can better understand it.

## Using `printf` to print unformatted text
You can pass an argument to the command without any format specifiers. For example, if I want the shell to display my full name, I can pass my name as an argument to the `printf` command.

```bash
printf "Ehoneah Obed"
```


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1654134008697/Ci2bpAXhk.png align="center")

The outcome is a bit messy. In that everything is jammed up onto a single line. To avoid such a problem, we have to introduce the newline formatter`\n` at the end of it.

```bash
printf "Ehoneah Obed \n"
```

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1654134080123/eiGbQqLg9.png align="left")

Can you spot the difference?

Now, let's try printing out a float with the `printf` command.

```bash
printf "2.555 \n"
2.555
```

Another way to write the above using a format specifier
```bash
printf "%f \n" 2.555
2.555000
```
What this command does is that, the shell will have to replace the `%f` with whichever value you pass as an argument (2.555 in this case). So, in essence, this is the same thing as the earlier one that we wrote. 

We can leverage the style for the last command above to specify the number of decimal places allowed.

To achieve that, you have to follow the `%` with a dot `.` and the number of decimal places you want to output before the `f`.

Example: Here is what you will get if you want to out the number 2.555 as a two decimal places float.
```bash
printf "%.2f \n" 2.555
2.56
```

You can therefore replace the number `2` in the command above and get your answer displayed in any given number of decimal places.

## Solution: Print a number with two decimal places, followed by a new line 
NB: The number will be stored in the environment variable MYNUM

This is going to be done just like the example we did above. You use the `printf` command with a float specifier `%f` but specify 2 decimal places, `%.2f`.

The full command with the variable MYNUM will look like this:
```
printf "%.2f \n" $MYNUM
```

### Conclusion
I hope this makes things clearer and you understand everything we did in order to arrive at the answer. If you have any questions, comment it below and I will respond to it. You can also make suggestions on how I can make such tutorials better for you.

Thanks for reading and I will love to connect personally with you. If you are on Twitter then you can [send me a DM](https://twitter.com/ehoneahobed)