## Write a C program that prints the last digit of the number stored in a variable

This question is a bit tricky for beginners, and you probably won't know exactly how to solve it. But as a programmer or a software engineer in the making, you are always developing your problem solving skills.

So, take some time and analyze the question well, and see if you can come up with a possible solution. 

Understanding the question is very important. So, what the question means is that, if I give you a variable that has been assigned a value of 25, I will need your program to print out 5.

So, what you need to worry about is how to get your program to see that it is 5 that is the last digit for it to print it out.

Before, we begin to code let's discuss any possible way to achieve this. The method that I am thinking of is:

```
if I divide the number given to me by 10, the remainder is always the last 
number. Examples: 

25/10 is equal to 2 remainder 5
70/10 is equal to 7 remainder 0
152/10 is equal to 15 remainder 2
```


Did you guess that?

> NB: To get the remainder of a number, the modulo operator `%` is used.

Once we now have an algorithm (method) to help us solve the question, we can develop pseudocode (not required but makes the final code writing part easier).

## Pseudocode to solve the problem
```
- Get the variable given (x)
- Declare y (remainder)
- y = x % 10
- print y
```

Now let's go ahead and write the actual code for the program.
> I will provide the first part of the code that generates the random variable, don't worry about that if you don't understand it. The solution to the problem will go below the comment `/* Our own code will go here */`

Here is the sample code that generates the random variable anytime the program is run.
```
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

int main(void)
{
      int x;

      srand(time(0));
      x = rand();

      printf("%d \n", x);

      /* Our own code will go here */
      return 0;
}
```

## Solution to the problem
```
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

int main(void)
{
      int x, y;

      srand(time(0));
      x = rand();

      /* Our own code will go here */

      y = x % 10;
      printf("The last digit of the number %d is %d \n", x, y);


      return 0;
}
```
After running the program above, the first outcome gotten is shown in the image below.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1654388874137/wtf7DsgYh.png align="left")

Voila! Our program is working perfectly telling us exactly what the last digit of the randomly generated number is.

### Conclusion
I hope you enjoyed reading this and it made you understand how to solve a problem like this. I would like to hear back from you. Is there anything I missed, or explained wrongly, or something you want me to elaborate more on?

Share with me what you also think. Mind you, I am also learning and your feedback will be valuable to me.

Thanks for reading and I would love to connect personally with you. If you are on Twitter, then you can [send me a DM](https://twitter.com/ehoneahobed) and let's have a good chat.