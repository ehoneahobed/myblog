## Monty Bytecode Interpreter using C

In order to practicalize our knowledge of data structures like stacks and queues in C language, we were tasked with building a C program that acts as a Monty bytecode interpreter. 


## What is the Monty Bytecode Interpreter 

This is a C program that will take a file as an argument, open the file, and read the instructions in the file, line by line. 

For each line read, the interpreter is supposed to execute the instructions on that line. 

The Monty bytecode is made up of special instructions and each line contains no or just one instruction. 

The instructions are in the form of various operations that can be performed on stacks or queues. 

Hence, the interpreter reads each line and performs the specific operation on a given stack or queue. 


## How to implement the Monty bytecode interpreter 

This looks very complex to implement, but we can break the whole project into simple parts that will make the implementation easier. 

Below are the steps that I used to implement the interpreter. 


### 1. Create a C program that accepts a file as an argument 

To be able to do this, you need knowledge of command line arguments in C language (Argc and Argv). You can check out this [live session](https://www.youtube.com/watch?v=iFMrxVWiTUs) that I held to get a better understanding of these.

%[https://www.youtube.com/watch?v=iFMrxVWiTUs]

Since the program needs to run with the name of a file as an argument, you would have to check if the end-user has provided a file or not. 

Every C program has a minimum of one command line argument, which is the name of the program itself. 

Your interpreter should therefore be expecting 2 arguments (the name of the program itself followed by the name or path to the file with the Monty bytecodes). 

You, therefore, have to check if Argc is equal to 2 before you proceed with any other thing. 

If it is more or less then you have to throw an error message because the person may be using the program wrongly. 


### 2. Check if the file can be accessed and open the file

Once, the end user is using your program as it's supposed to be used based on the earlier discussion then we have to now shift our focus to the file that the person provided. 

Remember that we expect the file to be a Monty bytecode file (ending with the extension ".m"). 

Before we even get into the file to check its content, we need to know where the file that has been provided is accessible. As in, if we have permission to open it in the first place. 

There is a standard C function that allows you to check whether a file is accessible or not. Use that function to check if you can access it. 

If you can't access it, then throw an error but if you can access it then move on to the next step. 


### 3. Open the file

Now that you know that you can access the file, you can go ahead and open the file.


**NB:** This isn't completed yet but my tight schedules is preventing me from continuing with it. I will continue as soon as I get some free time for it. You can always connect with me on [Twitter](https://ehoneahobed.com/twitter). 