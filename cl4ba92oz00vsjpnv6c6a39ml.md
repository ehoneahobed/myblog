## Functions & how to use them in C programming - Detailed Explanation

Let me start by using some analogies that you can easily understand, so we will build on them. 

## What are functions in computer programming
Do you remember how you were taught about verbs (action words)? For example, you know exactly what to do when I say 'walk'.

These action words are known as functions in computer programming. They tell the computer to take a certain action whenever they are called.

Your human brain has been programmed to understand what common verbs (or functions in computer language) mean. Walk, eat, sit, sleep, etc are all functions that your brain knows how to perform and doesn't need any further explanation.

In the same way, the computer (or compiler or interpreter for a particular programming language) has also been programmed to understand what certain functions mean. Examples in C programming include: `printf`, `scanf`, `putchar`, etc.

These kind of functions that are inbuilt are known as `system functions`. But to grant the programmer the ability to extend the actions a computer can take, a programmer is allowed to create his/her own function.

This is also possible in real life. Apart from the predefined action words that you know and understand, you can decide to create a word that only you and your close circle of friends understand (ever heard of bro code?).

For instance, the two of us can agree on a particular word and assign a meaning to it. Let's even go ahead and do the same. Let's use the word "**shattif**". Between you and I, when we say "**shattif**" it means, share to Twitter, Instagram and Facebook.

You realize that the two of us will understand this anytime we say it but every other person around us may be confused about what we mean. 

In the same way, you, as a programmer, can create your own custom functions that perform certain tasks when they are called. Such functions are called `user defined` functions.

The focus of this article will be more on the user defined functions. But the big question is, why will a user need to define their own functions?

## Importance of user defined functions in programming

1. User defined functions help programmers to easily reuse their code.
2. They help programmers reduce the complexity of their programs since they are able to break them down into large programs into smaller chunks of functions.
3. They also help programmers reduce the size of their programs by preventing code duplication.
4. They make code easy to maintain and debug.

Let's go on to take a look at how one can create and use such user defined functions.

With everything that I am going to share in this post, you will find in this video below which is an ALX peer discussion we had led by myself. So, if you prefer videos, then you can watch this video instead.

%[https://youtu.be/u40rF7zCYaQ]

## Functions in C programming

To be able to create and use your own custom functions in the C language, you have to understand 3 things. These three things are:

1. Defining a function
2. Declaring a function
3. Calling a function

## 1. How to define a function in C programming
Let me define a basic function that will add up two numbers and use it to explain how to define functions in C.

```C
int sum(int x, int y)
{
      return (x + y);
}
```

In the above function, there are a few things you need to pay attention to. The image below shows you exactly what makes up a function in the C programming language.

![my hashnode technical blog images (18).png](https://cdn.hashnode.com/res/hashnode/image/upload/v1654884358546/W1W6UmrUic.png align="left")

### Return Datatype
A function may or may not return some form of data but it is important to anticipate what type of data the function will be returning. The common datatypes that you come across are: `int`, `float`, `char` and `double`.

Hence, before even writing out what your function is going to do, you first have to state the type of data it will be returning. In the example above, we expect the function to return an integer (int).

### Name of function
You are allowed to call your function any way you want. It is however, recommended that you give your function a descriptive name. That means that the name you give your function should give a clue to what role the function will be playing.

In the example above, we called the function `sum` and that suggests that this function is going to do some sort of addition.

### Arguments of a function
Function arguments are predeclared variables that one can use inside the body of the function. 

A function can work with or without arguments. Anytime, you pass arguments to your function, you would have to specify the data type just as you do for the declaration of variables in your programs.

In the example above, we passed two arguments (`x` & `y`) to the function. We also declared them as integers. This means that anytime when the function is used, it is going to expect two integers as inputs inside the parathesis.

### Body of the function
This is where you tell us exactly what your function is going to do and how it is going to do it. You also provide a return statement if your function is expected to return something.

In the example above, the actual addition is done in the body of the function, and the outcome of the addition is returned.

## 2. How to declare a function
After defining your function, the next thing is to declare it. The essence of this is for other aspects of your program to know that such a function exist.

Note that, this function was just created by you so if you don't inform the other parts of your program, they wouldn't even know it to exist. I liken this to the use of a notice board.

After you have made a new publication, no one will no about it until you put it on the notice board for your colleagues to see it.

When it comes to declaring functions, it involves putting the prototype of the function at a particular place where the other files that need to use the function can see it.

If you intend to use the function in multiple files then it is recommended that you declare the function in a header file that will be shared by all those files.

A header file in C programming is just any file with a the `.h` extension which contains prototypes of functions and other important aspects of codes (to be discussed later).

What is important for you know is to know exactly what the prototype of a function is.

### What is the prototype of a function
The prototype of a function in C programming is a structure that tells the compiler what to expect in terms of return data type, and arguments whenever that function is used.

So, a function's prototype is expressed as `return data type` followed by the `name of the function` and a parenthesis with the `arguments` inside the parenthesis.

An example of prototype using the function we defined earlier is:
```C
int sum(int x, int y);
```

If you pay very close attention, you will realize that the prototype is the same as the very first line of the function's definition.

Hence, you can create a header file and put the above line of code in it. You can also put your prototype below your include statements in your other programs. An example will be:

```C
#include <stdio.h>

int sum(int x, int y);  /* declaration of the SUM function */ 

int main(void)
{
      // body of your main function goes here
}
```

## 3. How to call a function
Calling a function simply means using the function that you have created. To use the function, you just have to bring the name of the function followed by a parenthesis then the expected arguments of the function.

An example in our case can be `sum(2,3)`. With this example, we are going to receive the value `5` wherever we called the function. 

This is because per the definition that we gave the `sum` function, we expected it to return the sum of the two integers passed to it.

This means that we can go ahead and use our `sum` function in any program that we write and pass two numbers that we want to add to it for it to give as the sum.

After going through all the steps in creating and declaring functions, we can now use the function just as we use variables.

Examples:

- We can assign our function to a variable:
```C
int result;
result = sum(89, 92);
printf("%d \n", result);
```
The code above will give an output of:
```C
181
```

- We can also use our function directly inside other functions                                   :  
```C
printf("%d \n", sum(89, 92);
```
The above code will give us the same outcome as the earlier one.
```C
181
```

### Conclusion
I have tried my best to simplify functions, how to create and use them and it's my hope that it makes you understand those concepts very well. However, if you have any questions or clarifications, feel free to comment below or you can reach me via a [Twitter DM](https://twiter.com/ehoneahobed).

Also, even if you understand everything or know more than these, I will still love to hear your perspective about some of the things I shared here. So, do pass a comment or send me a [Twitter DM](https://twiter.com/ehoneahobed).