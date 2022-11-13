# Building a simple shell in C - Part 3

Our simple shell that we build from parts [one](https://blog.ehoneahobed.com/building-a-simple-shell-in-c-part-1) and [two](https://blog.ehoneahobed.com/building-a-simple-shell-in-c-part-2) are only able to show the user a prompt, read what they type, parse it into separate strings, and print the individual strings. It is unfortunately unable to execute the commands that the user types. What is the use of a shell if it cannot execute the command given to it?

That will be a useless shell, indeed. So, in this part, let's focus on how we can get our shell to execute the commands that are passed to it.

To be able to appreciate this functionality of the shell, you have to get a good understanding of how the Bash shell actually works. There are different types of commands that a shell executes. These commands will be implemented based on how they are actually implemented in the Bash shell. In the Bash shell, some commands are considered as:
- Built-in commands
- Binary Executable files
- Aliases

If you have some doubts about whether you understand the shell or not, then I encourage you to take a trip to [Stackoverflow](https://unix.stackexchange.com/questions/11454/what-is-the-difference-between-a-builtin-command-and-one-that-is-not) and read this very helpful thread:

%[https://unix.stackexchange.com/questions/11454/what-is-the-difference-between-a-builtin-command-and-one-that-is-not]

In this simple shell project, we will be implementing built-in commands, executables, and aliases, so you need to understand what each of them is to appreciate what we will be doing subsequently in this project.

For now, we will only focus on getting the executables working and later refactor our codes to take other forms of commands into account.

Let's get started implementing the execution functionality of our shell.

## How to execute the given command
Now that we have been able to read the command that was input, we can use any of the exec system calls to execute the command. The exec family has quite a number of these calls, and their usage differs slightly from each other. You can read more about them [here](https://linuxhint.com/exec_linux_system_call_c/).

In my project, I was restricted to the use of `execve` and therefore, I will focus on using that even though using the others seems a lot more easier.

As with everyone of the other standard library functions or system calls, we need to use the man pages to guide us on their usage.

Run `man execve` and read on it to get a hold of what I am about to do.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1668339211594/FMsYeyRgz.png align="left")

>NB: Take note of the part of the description that says **"This causes the program that is currently being run by the calling process to be replaced with a new program..."**. For now, I will ignore it but we will tackle it in subsequent parts when we talk about `forking`.

From the prototype of the `execve` function, we need to pass three arguments; `pathname`, `argv` and `envp`.

The `pathname` represents the command that the end user inputs, which is expected to be a binary executable or an executable script. We have already dealt with the first two arguments. From the previous post, we generated `argv` and the command is the first string in `argv`. Hence, the `pathname` will be `argv[0]`.

The problem with this is that, `execve` expects `pathname` to always be a path. Hence, if the user types just the name of the file, it's not going to be able to execute it.

When `execve` is run, it checks the the third argument (`envp`) provided to see if a path like what was given actually exists. If it exists, the file will be executed. Otherwise, it returns (-1) to indicate a failure.

Before, we jump on to start coding, let's deal with the `envp` part of `execve`. 

## What are environment variables and how to use them in C programs
These are variables that are created and maintained at the operating system level. Programs executed from the shell inherit all of the environment variables from the shell. Inside this environment variables, we have the PATH variable, which will enable `execve` to find the right path to execute the command.

In your C program, there are two ways to get access to the environment variables. The first is through using the prototype of the main functions that has `envp` as a parameter. The second option is through the global variable `environ`.

Using `envp` has a few limitations when you are going to be passing the environment variable to various functions in separate files. We will therefore stick to using `environ`.

## How will the shell execute the commands
Most commands that are executed in a Linux environment are simply executable files. You can think of them as C files that have been compiled to make them executable. These files are kept within special directories, and the paths of these directories are all collected into the `$PATH` variable which we can access through the environment variables. 

The `$PATH` variable, therefore, is a string that has a list of all the relevant directories that you want your `shell` to search through when it receives a command, and each of these directories is separated by a colon in the string.

To take a look at what your $PATH variable holds on your system, type `echo $PATH`.

On my system the output I get is as below:
```Bash
echo $PATH
/home/ehoneahobed/.local/bin:/home/ehoneahobed/.local/bin:/home/ehoneahobed/.local/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin
```

### How will my shell know which of the directories to use
The shell will basically append the command that was given to each of these directories to see if the file exists in that directory. If it exists in that directory, it will go ahead and execute the file but if not then it gives you an error message `No such file or directory found`.

Let's get started with the coding part.

## Using `execve` to execute the command
First of all, let's add the required header file (obtained from the man page) to our `main.h` file. Your main.h file should now look like this:
```C
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
```
Let's create a new file that will be responsible for handling the command execution. We will call the file `execmd.c`. Just to illustrate how this is going to work, let's start with a basic one where we won't be handling the environment variables and getting the exact path.

This step is being implemented just so you fully understand what is happening when we start implementing the required ones.

The prototype we will use for the function is `void execmd(char **argv)`. This means that we will call the `execmd()` function in the `main.c` file and pass the `argv` as an argument. Also, you need to add the prototype to your `main.h` file.

For now, your new file, `execmd` looks like this:
```C
#include "main.h"


void execmd(char **argv){
    
}
```
We will also go ahead and delete the piece of code that we used to test our previous `main.c` code. `main.c` should now look like this:

```C
#include "main.h"

int main(int ac, char **argv){
    char *prompt = "(Eshell) $ ";
    char *lineptr = NULL, *lineptr_copy = NULL;
    size_t n = 0;
    ssize_t nchars_read;
    const char *delim = " \n";
    int num_tokens = 0;
    char *token;
    int i;

    /* declaring void variables */
    (void)ac;

    /* Create a loop for the shell's prompt */
    while (1) {
        printf("%s", prompt);
        nchars_read = getline(&lineptr, &n, stdin);
        /* check if the getline function failed or reached EOF or user use CTRL + D */ 
        if (nchars_read == -1){
            printf("Exiting shell....\n");
            return (-1);
        }

        /* allocate space for a copy of the lineptr */
        lineptr_copy = malloc(sizeof(char) * nchars_read);
        if (lineptr_copy== NULL){
            perror("tsh: memory allocation error");
            return (-1);
        }
        /* copy lineptr to lineptr_copy */
        strcpy(lineptr_copy, lineptr);

        /********** split the string (lineptr) into an array of words ********/
        /* calculate the total number of tokens */
        token = strtok(lineptr, delim);

        while (token != NULL){
            num_tokens++;
            token = strtok(NULL, delim);
        }
        num_tokens++;

        /* Allocate space to hold the array of strings */
        argv = malloc(sizeof(char *) * num_tokens);

        /* Store each token in the argv array */
        token = strtok(lineptr_copy, delim);

        for (i = 0; token != NULL; i++){
            argv[i] = malloc(sizeof(char) * strlen(token));
            strcpy(argv[i], token);

            token = strtok(NULL, delim);
        }
        argv[i] = NULL;

        /* execute the command */
        execmd(argv);

    } 


    /* free up allocated memory */ 
    free(lineptr_copy);
    free(lineptr);
    
    return (0);
}
```

In the `execmd` function, let's confirm that `argv` isn't empty and grab the first string in `argv`. That will be the string at index 0 and it is supposed to be the command to be executed.

Since, we are not bothering about the environment variables for now, we will pass `NULL` in its place inside the `execve` function. We will also check if the `execve` function executed successfully or returned with an error. We will go ahead and print the error message if there was one.

Here is what the code currently looks like for the `execmd.c` file.
```C
#include "main.h"

void execmd(char **argv){
    char *command = NULL;

    if (argv){
        /* get the command */
        command = argv[0];

        /* execute the command with execve */
        if (execve(command, argv, NULL) == -1){
            perror("Error:");
        };
    }
    
}
```
Let's compile our code and test it out. Since, we have added a new file, we will need to include that file in our command for compilation.
```Bash
gcc -Wall -Wextra -Werror -pedantic main.c execmd.c  -o eshell
```
Here is a screenshot of the testing I did on mine.


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1668347181115/x4YdDNllA.png align="left")

From my test cases, I used the `ls` command and there are three important things to take note of (which will influence how we proceed with the project).

1. I get an error (no such file or directory) when I use just the command `ls`.
2. It works perfectly when you pass the full path of the command.
3. When the `execmd()` executes successfully, it breaks the loop and exists from our shell.


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1668348835089/DNgFY1LX3.png align="left")

The inference therefore is that for our shell the work properly, users must always enter the full path of the command they want. What kind of shell does that?

We need to fix that because no body will be willing to use such a shell. Your users cannot memorize the path for all the commands they will bee using.

Do you remember the note I gave about the use of `execve` from its man page? That is what is responsible for the third point listed. After the execution of a command, we don't want to break out of the loop but rather show a new prompt for users to be able to enter new commands continuously. We will tackle this later.

For now, you can play with your simple shell. In the next part, I will cover how to generate the full path for every command that your users enter on the shell. For the time being, if you want to know the exact path of any bash command, run `which <command name>` on the bash terminal.

For example:
```Bash
>>> which ls
/usr/bin/ls

>>> which echo
/usr/bin/echo
```


<hr>

## Changes that I had to make to the codes from previous parts:
To correct some issues with **segmentation fault** and **double free detected error**, I made the following changes to our previous code base.
a. Remove the `free()` from the while loop and place it outside just before the `return` statement.
b. Added `free(lineptr_copy)`

You can check the previous posts out with the links below:
- Part 1

%[https://blog.ehoneahobed.com/building-a-simple-shell-in-c-part-1]

- Part 2

%[https://blog.ehoneahobed.com/building-a-simple-shell-in-c-part-2]

## Conclusion
Gradually, we are getting close to building a functional miniature version of the Bash shell. All codes are available on GitHub for those who would need it and those who make want to contribute to it as well.

If you're like the content and would love to support me, then show some love by following me on this [blog](https://hashnode.com/@ehoneahobed) and also subscribe to my [YouTube channel](https://youtube.com/@ehoneahobed.com?sub_confirmation=1). I will soon make this series into videos as well so if you would like to see the videos, then turn on post notifications for my youtube channel.

You can also send me a [DM on Twitter](https://ehoneahobed.com/twitter) if you would like to connect with me personally. 