## Write a script that runs a C file through the preprocessor and saves the result into another file

My first day of learning C programming was exciting because I had heard so much  about the C programming language and couldn't wait to start. 

The very first task that we were given was to write a script that runs a C file through the preprocessor and saves the result into another file.

In this article, I am going to explain how to go about a task like this. To begin with, let's get a practical question to work towards.

```bash
Write a script that runs a C file through the preprocessor and saves the result into another file.

Work with the following assumptions:

The C file name will be saved in the variable $MYFILE
The output should be saved in a file called 'interm'
```
To solve this problem, there are a few things we will need to understand. The most important of these is understanding the question itself. There are three parts to the question that you need to understand to answer correctly.

So, what does the question demand of us? 

## What does the question actually mean?

If you are a student taking the same course that I am taking or have been following my write-ups, you will know that this is coming right after learning about shell scripting.

This means that the first part of the question that says "write a script that runs a C file" is referring to writing a [bash script](https://medium.com/@ehoneahobed/how-to-write-a-script-that-performs-certain-commands-in-linux-ad4d9681a470).

The second part of the question is "runs a C file through the preprocessor". If you know anything about the C language then you will agree with me that it is a compiled language.

Hence, programs written in C need to be compiled before execution. This compilation process is broken down into 4 major steps;

- Preprocessing
- Actual Compilation
- Assembly
- Linking

Each of the steps above yields a different output, and this question is asking us to write a script that will produce the output from the preprocessing.

Hence, we are going to focus on just the preprocessing in this article. I will address the other steps in subsequent articles where I answer their respective questions.

## What is preprocessing in C programming?
In the process of compiling any C program, preprocessing is where all the header files and macros that were used in the program are processed and added to the actual program.

You remember how you always begin your C program with the code below;
```c
#include <stdio.h>
```

Any part of your C program that begins with `#` is meant for the preprocessor. The initial code above tells the preprocessor to include the standard input output header (stdio.h) file.

So, the first step that your C program goes through is to go and get that header file and every other header file as well as macros that you introduce in your program.

After this is done, a new file is generated, which will then be passed on for the actual compilation process (yet to be discussed—check next article).

## How do I get my C program to be preprocessed?
Knowing the answer to this question, "How do I get my C program to be preprocessed?", will help you solve the practical question that was given at the beginning of this article.

There are a number of compilers that can be used but one common one which is available by default in almost all Linux distributions is the GNU Compiler Collection (GCC).

Hence a simple `gcc` command can be used to compile (any of the 4 compilation processes mentioned earlier) your C program.

However, by default, the `gcc` command does all the 4 steps together and gives you the final executable file.

If you are looking for just one or more of the intermediate processes' outcomes, then you would have to introduce some options to the `gcc` command.

Since we are interested in the preprocessing step in this article, we will focus on the option for preprocessing only and tackle the rest in subsequent write-ups.

## What `gcc` option is used for just preprocessing?
Linux commands can take up several options, but each command has specific mentions and what they mean. You can get details on each command by checking the man pages or even using the help option.

Options for a Linux command are introduced with a single hyphen (-) if it is one character and a double hyphen if it is a complete word (more on this later).

To make sure your `gcc` command performs just the preprocessing, you will have to give it the `-E` option. So, a typical command to take a C program through only preprocessing will be like:

```
gcc -E name_of_file
```
where name_of_file is the name of the file containing the source code which is expected to be a C program.

Now that you have grasp the understand and how to solve the second part of the question, let's take a look at what the third part means.

The third part of the question "saves the result into another file".

## How can I save the preprocessed C file into another file
One of the attributes that the `gcc` command expects is the name of the output file preceeded by the option (-o).

By default, the `gcc` command will produce an output with the same name. But if you want it to give the output file a special or different name, then you would have to explicitly tell it to do so.

How you do that is by introducing the option -o with an attribute being the name of the file. In the question that we are solving, we were told that the output file should be called `interm`. Hence, our command will look like:

```
gcc -E name_of_file -o interm
```
The above command simply means, preprocess the C program in the file called `name_of_file` and give the preprocessed file the name `interm`.

Now, let's put all this together to solve the problem that we were given.

## Solution to the practical question
The question was
```bash
Write a script that runs a C file through the preprocessor and saves the result into another file.

Work with the following assumptions:

The C file name will be saved in the variable $MYFILE
The output should be saved in a file called 'interm'
```

If you don't know how to write a bash script then check out [my previous post on how to do that](https://medium.com/@ehoneahobed/how-to-write-a-script-that-performs-certain-commands-in-linux-ad4d9681a470).

It is also worth noting that the C file which is to be our source code has been saved into a variable called `$MYFILE`. This means that you should replace the name of the source code file in your command with the variable `$MYFILE`.

The solution thus will be like:
```bash
#!/bin/bash
gcc -E $MYFILE -o interm
```
### Conclusion
I hope you enjoyed reading this and made you understand how to solve a problem like this. I would like to hear back from you, is there anything I missed, or explained wrongly or something you want me to elaborate more on?

Share with me what you also think, mind you I am also learning and your feedback will be valuable to me.

Thanks for reading and I will love to connect personally with you. If you are on Twitter then you can [send me a DM](https://twitter.com/ehoneahobed) and let's have a good chat.