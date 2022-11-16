# Building a simple shell in C - Part 4

Up until the end of [Part 3](https://blog.ehoneahobed.com/building-a-simple-shell-in-c-part-3) of the series, our shell was able to show a `prompt` for the end user to type some commands, `read`, `parse` and `execute` the command, except that the user had to explicitly provide the path for each command they wanted to execute.

In this part, we want to focus on generating the path for each command ourselves.

Here is what our simple shell looks like so far in terms of files created and the codes in them. We have 3 files so far (`execmd.c`, `main.c`, and `main.h`).

For `execmd.c`, here are the codes:
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
        }
    }
    
}
```

For `main.h`, here are the codes in it:
```C
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>

void execmd(char **argv);
```

For `main.c`, here are the codes in it:
```C
#include "main.h"

int main(int ac, char **argv)
{
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
    while (1)
    {
        printf("%s", prompt);
        nchars_read = getline(&lineptr, &n, stdin);
        /* check if the getline function failed or reached EOF or user use CTRL + D */
        if (nchars_read == -1)
        {
            printf("Exiting shell....\n");
            return (-1);
        }

        /* allocate space for a copy of the lineptr */
        lineptr_copy = malloc(sizeof(char) * nchars_read);
        if (lineptr_copy == NULL)
        {
            perror("tsh: memory allocation error");
            return (-1);
        }
        /* copy lineptr to lineptr_copy */
        strcpy(lineptr_copy, lineptr);

        /********** split the string (lineptr) into an array of words ********/
        /* calculate the total number of tokens */
        token = strtok(lineptr, delim);

        while (token != NULL)
        {
            num_tokens++;
            token = strtok(NULL, delim);
        }
        num_tokens++;

        /* Allocate space to hold the array of strings */
        argv = malloc(sizeof(char *) * num_tokens);

        /* Store each token in the argv array */
        token = strtok(lineptr_copy, delim);

        for (i = 0; token != NULL; i++)
        {
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

To help us generate the path for each command that is typed, we will create a separate file to hold our function that will do that job. If you are familiar with the Linux environment, then you can say that this function we are about to create works like the `which` Linux command.

Let's call our function `get_location.c`. So, go ahead and create a new file and name it as such. 

## How to create the `get_location` function
This function is expected to take in the command that was passed (eg: `ls`) and return the path of that command (eg: `/usr/bin/ls`). The prototype of this function will therefore have a `char *` as both the return data type and the parameter/argument since both are strings.

`char *get_location(char *command);` will be the prototype for our function. Go ahead and add this to the `main.h` file.
```C
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>

void execmd(char **argv);
char *get_location(char *command);
```
To help us get the path for the given command, we first have to access the environment variable PATH and it's value. The value of this PATH variable, as explained in part 3 of this series is a string with all the various paths that your shell searches through by default where each path is separated by a colon (`:`).

In a Linux terminal, you can check this PATH variable by typing the command `echo $PATH`. When I type this on my terminal, this is the output and yours may be very similar.
```Bash
PATH=/home/ehoneahobed/.local/bin:/home/ehoneahobed/.local/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin
```

In the C language, there is a function that allows us to get the value for this environment variable. Let us start off by creating a variable to which we will assign the path obtained from the environment variables from.

We will call our variable `path` and along the line we will need to keep a copy of it (I will explain why soon) so we will also create a `path_copy` variable.

Our `get_location.c` file should therefore start like this:

```C
#include "main.h"

char *get_location(char *command){
    char *path, *path_copy;
    
}
```

## How to get the value of the `PATH` environment variable in C
The function that we can use to get the PATH environment variable is `getenv()`. As we always do, let's check the man page for this function and see how we can use it.
```Bash
man getenv
```


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1668565200561/SGzOoLQBZ.png align="left")

Per the description from the man page, this function searches the environment list to find the specific environment variable name which you pass to it as argument. The prototype for the function is `char *getenv(const char *name)` and it returns a pointer to the value in the environment, or NULL if there is no match.

In our case, the variable we are targeting is `PATH` so we can write the function as such
```C
getenv("PATH")
```

But we already created our own variable `path` that we will be assigning the return value of `getenv()` to. So it finally looks like this when added to our `get_location()` function.
```C
#include "main.h"

char *get_location(char *command){
    char *path, *path_copy;

    path = getenv("PATH");
}
``` 
## Create a duplicate of the `path` 
I mentioned this earlier but haven't explain why we will need a duplicate of the path. To finally help us get the path for each command, we will be using the `strtok` function and if you remember anything about that function, it should be its destructive nature. Strtok breaks down a string into its component words or collection of characters based on a specified delimiter.

With the help of the `strdup()` function, we can easily create the new copy of `path`. If you are not familiar with `strdup()`, go ahead and check the man page for it (`man strdup`). This function will [dynamically allocate memory](https://youtu.be/-za3kDtaMvY) for you so remember to free that memory when you are done using your variable holding its return value (`path_copy` in our case).

```C
path_copy = strdup(path);
```

## How to generate the path for the given command 
In order to generate the path for the given command, we will need to follow the steps below:
- Get the length of the command given
- Break down the path into individual tokens
- Run a loop in which we append a forward slash (`/`) followed by the `command` then a NULL terminating character (`\0`). After which we test the outcome to see if it is a valid path before returning it.

Let's take each step and implement it.

### Step 1: Get the length of the command

Create a new variable `command_length` and use the `strlen()` function to get the length of the given command.
```C
command_length = strlen(command);
```

### Step 2: Break down the path_copy variable into individual tokens
As already mentioned, the individual paths within this path_copy variable are separated by colons (`:`).

We can therefore use the `strtok` function with `:` as the delimiter. We will also need to create a variable that will hold the return value of `strtok`. Let's call that variable `path_token`.

```C
path_token = strtok(path_copy, ":");
```

### Step 3: Run a while loop to get and test the exact path for the command
In this while loop, you have to check if the `strtok` function hasn't returned NULL because as soon as it does it means we have gotten to the end of the path variable.

Since for each of the paths obtained by breaking down `path_copy`, we are going to append a forward slash, the command and a NULL terminating character. We need to allocate memory for a new string that will hold these.

We can achieve this with the `malloc` function. But to do this, we will need to know the exact size to allocate. Already, we have obtained the length of the command. We will therefore proceed to find the legth of each token obtained from `strtok` and add the number `2` to it since we will be introducing 2 extra characters (forward slash and NULL character).

Create a variable `directory_length` which should be of integer type and another variable `file_path` that will serve as the string holding the full path.
```C
directory_length = strlen(path_token);
file_path = malloc(command_length + directory_length + 2); 
```
After this, we can use the `strcpy` function to copy the token obtained into the new `file_path` variable. You can then go ahead to append the `/`, `command` and `\0` in the respective order with the help of the `strcat` function.

```C
strcpy(file_path, path_token);
strcat(file_path, "/");
strcat(file_path, command);
strcat(file_path, "\0");
```
By doing the above, we now have a complete file path to any command that was entered. The problem is that we are creating the file path from each of the directories available in the PATH environment variable. We should therefore check each of them and only return the one that is truly the path for the given command.

To be able to test it, we introduce a new function the `stat` function. I will let the man page do all the talking so quickly check it out for yourself.
```Bash
man 2 stat
```

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1668569084039/I_itE1APR.png align="left")

From the man page of `stat`, there are a few header files that we need to add to our `main.h` file for it to work. These are:
- #include `<sys/types.h>`
- #include `<sys/stat.h>`
- #include `<unistd.h>`

The prototype for the `stat` function is `int stat(const char *pathname, struct stat *statbuf);`. The function is supposed to return information about a file in the buffer pointed to. Since, the commands we are targeting are executable files, this function will help us test whether the file path that we have created exists or not. 

The function returns zero when it successfully access the file path provided but returns -1 when it fails.

We therefore need create a variable that will serve as the buffer where the testing will be done. Let's call that variable `buffer`. We can then go on to test the `file_path` that we generated. The code for that will look like this:

```C
if (stat(file_path, &buffer) == 0){
/* return value of 0 means success implying that the file_path is valid*/
/* free up allocated memory before returning your file_path */
      free(path_copy);

      return (file_path);
 }
```
However, if the file doesn't exist then we have to discard what we stored in `file_path` and generate a new `file_path` with the next directory if we have not yet tried all the directories in the PATH environment variable.

If we don't get any match after going through all the directories and exiting the while loop, we will just return the command as it was passed to 

When you add all the new codes to the `get_location.c` file, we get this:

```c
#include "main.h"

char *get_location(char *command){
    char *path, *path_copy, *path_token, *file_path;
    int command_length, directory_length;
    struct stat buffer;
    
    path = getenv("PATH");

    if (path){
        /* Duplicate the path string -> remember to free up memory for this because strdup allocates memory that needs to be freed*/ 
        path_copy = strdup(path);
        /* Get length of the command that was passed */
        command_length = strlen(command);
        
        /* Let's break down the path variable and get all the directories available*/
        path_token = strtok(path_copy, ":");

        while(path_token != NULL){
            /* Get the length of the directory*/
            directory_length = strlen(path_token);
            /* allocate memory for storing the command name together with the directory name */
            file_path = malloc(command_length + directory_length + 2); /* NB: we added 2 for the slash and null character we will introduce in the full command */
            /* to build the path for the command, let's copy the directory path and concatenate the command to it */
            strcpy(file_path, path_token);
            strcat(file_path, "/");
            strcat(file_path, command);
            strcat(file_path, "\0");

            /* let's test if this file path actually exists and return it if it does, otherwise try the next directory */
            if (stat(file_path, &buffer) == 0){
                /* return value of 0 means success implying that the file_path is valid*/

                /* free up allocated memory before returning your file_path */
                free(path_copy);

                return (file_path);
            }
            else{
                /* free up the file_path memory so we can check for another path*/
                free(file_path);
                path_token = strtok(NULL, ":");

            }
        
        }

        /* if we don't get any file_path that exists for the command, we return NULL but we need to free up memory for path_copy */ 
        free(path_copy);

        /* before we exit without luck, let's see if the command itself is a file_path that exists */
        if (stat(command, &buffer) == 0)
        {
            return (command);
        }


        return (NULL);
    
    }


    return (NULL);
}

```

> **NB**: Ideally, we are supposed to check the command to make sure it isn't a `built-in` command or an executable script or an `alias` before we go ahead to generate the path. But I haven't done that yet because we are yet to handle those ones. We will refactor the code to include those in subsequent parts of the series.

## Testing the current version of the simple shell
In order to test the current state of our simple shell, we have to make use of our `get_location` function in the `execmd.c` file.

In `execmd.c`, we will create a new variable (`actual_command`), assign the return value of `get_location` to it and pass `command` to it as an argument. 

The `execmd.c` file will now look like this:

```C
#include "main.h"

void execmd(char **argv){
    char *command = NULL, *actual_command = NULL;

    if (argv){
        /* get the command */
        command = argv[0];

        /* generate the path to this command before passing it to execve */
        actual_command = get_location(command);

        /* execute the actual command with execve */
        if (execve(actual_command, argv, NULL) == -1){
            perror("Error:");
        }
    }
    
}
```

Now, we need to recompile our files. Since the number of `.c` files are increasing and we don't want to keep changing our command for compilation all the time, we will stick to using a wildcard for selecting all `C` files. The command for compilation now becomes:
```
gcc -Wall -Werror -Wextra -pedantic -std=gnu89 *.c -o eshell
```
After compilation, go ahead and execute your shell (`./eshell`) and try it with some commands. This is what I get at my end when I try it.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1668574032139/jPFMu-B3h.png align="left")

The challenge of our shell exiting after a successful execution of each command still persists and as I explained earlier, it is because of the way `execve` works. We will fix that later when we look at `forking`.

For now, let's celebrate how far we have come with this project. We have a functional shell but it needs a lot of improvements though. We will continue in the next part.

You can access the codes for this project on GitHub using the link below:

%[https://github.com/ehoneahobed/eshell]

## Conclusion
I hope you are enjoying the series? Give me your feedback by commenting below. I can't wait to finish the whole series and see what our simple shell turns out to be. 

If you appreciate my work and would want to show me some love then go ahead and subscribe to my [YouTube Channel](https://youtube.com/@ehoneahobed?sub_confirmation=1). In fact, I will be turning this into a video series where I show up and build various projects. So, do well to also turn on your post notifications for my channel so you don't miss out on any of them.

Also, follow me here on [my blog](https://hashnode.com/@ehoneahobed). If you would love to connect with me personally, you can do that through [Twitter](https://ehoneahobed.com/twitter). I would love to hear from you. Thanks  so much for spending your time reading this post, I really appreciate you for that.