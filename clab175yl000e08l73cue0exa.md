# Building a simple shell in C - Part 2

In part one of the building a simple shell in C, we ended up building a shell whose only job was to present a prompt for a user to enter some text and return that same text. That is a pretty useful shell for now and we want to make it more useful starting from this second part.

%[https://blog.ehoneahobed.com/building-a-simple-shell-in-c-part-1]

The first problem that we identify with our current state of the shell is that, immediately after printing out what the end user types, the shell exits. The solution to this problem will be to put that operation into an infinite loop, which will keep showing the prompt after each execution so the user can type in another command.

All the codes for the entire series is currently available on GitHub

%[https://github.com/ehoneahobed/eshell]

I will be creating a video series showing exactly what we are building with this blog series. If you are interested in seeing the videos, then subscribe to my [YouTube channel](https://youtube.com/@ehoneahobed?sub_confirmation=1) and turn on post notification.

## Adding an infinite loop to the shell
Let's therefore go ahead and implement that infinite loop. To create an infinite loop, we can use the while loop and check for a statement or expression which will always evaluate to true. An example will be `while(1)`. One in this context will always remain one and nothing is going to change it. For that matter, the loop is going to execute it forever.

We will later learn how to break out of that loop when we start implementing commands like `exit`, etc.

Let me first show you the final state of our code from part 1 before I make the necessary modifications.

```C
#include "main.h"

int main(int ac, char **argv){
  char *prompt = "(Eshell) $ ";
  char *lineptr;
  size_t n = 0; 

  /* declaring void variables */
  (void)ac; (void)argv;

  printf("%s", prompt);
  getline(&lineptr, &n, stdin);
  printf("%s\n", lineptr);

  free(lineptr);
  return (0);
}
```

Let's go ahead and add the infinite loop.
```C
#include "main.h"

int main(int ac, char **argv){
  char *prompt = "(Eshell) $ ";
  char *lineptr;
  size_t n = 0; 

  /* declaring void variables */
  (void)ac; (void)argv;

    /* create an infinite loop */
    while (1){
      printf("%s", prompt);
      getline(&lineptr, &n, stdin);
      printf("%s\n", lineptr);
       
      /* free up allocated memory */
      free(lineptr);    
    }
 
  return (0);
}
```
Let's test our code and see if it is now working the way we want it to but before you do that, you have to first recompile your code. Use the command below to recompile the code.
```Bash
gcc -Wall -Wextra -Werror -pedantic main.c -o eshell
```

After recompiling, go ahead and run the executable file `eshell`.
```
./eshell
```
Here is the output. A new prompt is provided anytime that I click Enter after typing out a command.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1668064308778/uYZFpxGIu.png align="left")

## Exiting the shell
Let's do one more cleaning up before we continue. The `getline` function can fail when trying to read what was typed. It mostly fails when it reaches an end of file (EOF) character or when a user uses the keyboard shortcut `CTRL + D`.

In both of those instances, it is an indication that we should exit from the shell. So, let's implement that functionality.

We now need to pay attention to the man page for `getline`. If you have forgotten what we saw from part one of this series then just run the command below in your terminal to check it out.
```Bash
man getline
```
Inside our `main.c` file, we need to create a new variable that will hold the return value of the `getline` function. This is supposed to be the total number of characters that were read by the function. It is however `-1` if it fails or encounter the EOF character.

Thus, we will check if the return value is `-1` and exit the shell if it is. let's call the variable `nchars_read` and according to the man page, it should be of type `ssize_t`. Let's add these modifications to our code.

```C
#include "main.h"

int main(int ac, char **argv){
  char *prompt = "(Eshell) $ ";
  char *lineptr;
  size_t n = 0; 
  ssize_t nchars_read;

   /* declaring void variables */
  (void)ac; (void)argv;

    /* create an infinite loop */
    while (1){
      printf("%s", prompt);
      nchars_read = getline(&lineptr, &n, stdin);
      /* check if the getline function failed or reached EOF or user use CTRL + D */ 
        if (nchars_read == -1){
            printf("Exiting shell....\n");
            return (-1);
        }

      printf("%s\n", lineptr);

      /* free up allocated memory */
      free(lineptr);    
    }

  return (0);
}
```
Great job so far. Recompile the code, and let's test it out by clicking `CTRL + D` when the prompts shows up.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1668066540296/LNpsmaDkE.png align="left")

As you can see, the shell printed out `Exiting shell...` right after I clicked `CTRL + D`. Note that you can decide to exit the shell quietly without printing anything out to the screen. That's how most shells work but I just wanted you to see the effect of the code that is why I printed out `Exiting Shell...`.

## Parsing commands typed into the shell
The next step after reading whatever the user types into your shell is to break the command into individual strings so we can execute them as commands. For instance if someone types `cat main.c` into the terminal. we want to grab that and break it into two strings `cat` and `main.c`.

The process of doing that is called parsing or we can refer to it as tokenization (converting a single string into tokens of strings).

There is a standard library function `strtok` that does just that for us. To proceed, you have to understand how `strtok` works. Start by checking out the man page for `strtok`.
```Bash
man strtok
```

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1668066813889/T7lIDyGHx.png align="left")

To have access to that function's prototype so we can use the function in our code, we need to add the `string.h` header file.
```C
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
``` 

Also, to use the `strtok` function in our code, we need to understand what the prototype requires of us.
`char *strtok(char *str, const char *delim);`

> **str** represents the string to be tokenize

> **delim** represents what can of characters we expect to be separating the string which should be used as a guide to break the string into smaller chunks.

For example, if the end user types `cat main.c` then we want to break this string into two separate strings. You realize that it is the space that separates the two strings. Hence, in this case:

> **str** = "cat main.c"

> **delim** = " "

In our case, the string to be tokenized is what was read earlier by the `getline` function. Do you remember the particular variable was used to store that string? It was the variable `lineptr`. But since `strtok` breaks down the string, we need to create a copy of it to use.

So, let's create a new variable to hold the delimiters that we will use. For now, we will consider an empty space and the new line character as the possible delimiters.

Then create another variable to hold the copy of the string to be passed to `strtok`.  We will call that variable `lineptr_copy`.

```C
char *lineptr_copy = NULL;
const char *delim = " \n";
```
Add the above line of code to your `main.c` file.
```C
 #include "main.h"

int main(int ac, char **argv){
    char *prompt = "(Eshell) $ ";
    char *lineptr = NULL, *lineptr_copy = NULL;
    size_t n = 0;
    ssize_t nchars_read;
    const char *delim = " \n"

    /* declaring void variables */
    (void)ac; (void)argv;

    /* Create a loop for the shell's prompt */
    while (1) {
        printf("%s", prompt);
        nchars_read = getline(&lineptr, &n, stdin);
        /* check if the getline function failed or reached EOF or user use CTRL + D */ 
        if (nchars_read == -1){
            printf("Exiting shell....\n");
            return (-1);
        }

        printf("%s\n", lineptr);

        /* free up allocated memory */ 
        free(lineptr);
    } 


    return (0);
}
```

It's been great so far, but I need you to pay close attention to the next few steps so you don't miss out on any important detail. Here is a summary of the steps ahead:
- Dynamically allocate space to store the copy of `lineptr`
- Make the copy of the `lineptr` string
- split the copied string into an array of strings
 - calculate the total number of tokens that are expected
  - With the total number of tokens in mind, allocate enough space to hold an array of all those strings as the argument vector (argv)
  - Store each token generated in its rightful position in the array

Let's implement each of those steps.

### Dynamically allocate space to store a copy of the string read
To allocate the space, we need to use the `malloc` function. If you don't already know how to use the `malloc` function, you can check out the man pages. to learn about it. Remember that we will need to free up the space we allocate after its work is done.

To create an adequate space for the string, we need to know the exact size in bytes. The `getline` function returns the number of characters contained in the string. We can therefore multiply the return value of the `getline` function (`nchars_read`) by the size of a char in bytes to get the actual size in bytes for the whole string. 

```C
lineptr_copy = malloc(sizeof(char) * nchars_read);
if (lineptr_copy== NULL){
        perror("tsh: memory allocation error");
        return (-1);
}
```

### Make a copy of the `lineptr`
Another function `strcpy` is needed for the copying. It takes two arguments (a pointer to the allocated space and the string to be copied). These two pointers in our case are `lineptr_copy` and `lineptr`.

```C
strcpy(lineptr_copy, lineptr);
```

### Calculate the total number of tokens expected from the string
This is where we are going to use the `strtok` function to break down the string into individual tokens and count the number of tokens. This is the main reason why we needed to create a copy of the string. 

We are just counting with the help of the `strtok` function but it is going to destroy the string eventually. We therefore need to reserve a copy which we will use for getting each token and storing them in an array.

Let's create two new variables `num_tokens` to serve as the counter and `token` to store the token generated by `strtok`.

> **Important Note about the use of `strtok`**
<br \><br \>The first time you use `strtok`, it starts reading from the very first character and ends when any of the delimiters are met. 
<br \><br \>The next call to `strtok` will start from  exactly where the break ended for the first string. <br \><br \>You can think of it this way: The initial string was broken off and no longer part of the string passed to strtok.

Now, let's see how that will be implemented in code.
```C
/* split the string (lineptr) into an array of words */
        token = strtok(lineptr, delim);

        /* determine how many tokens are there*/
        while (token != NULL){
            num_tokens++;
            token = strtok(NULL, delim);
        }
        num_tokens++;
```
**Further explanations of the above code:**
We get the first token when we run strtok for the first time. Then we check if that token received is not null. If it is not null we add one to our counter `num_tokens` which was initially set to zero.

After that, we call `strtok` again so that we can get the next token. Once another token is gotten, we proceed to check if it is not null with the help of the while loop. Add one to the counter and keep repeating the process till no more tokens are generated.

At that point `token` becomes null and we break out of the while loop.

### Allocate space to hold the array of strings (tokens)
We will use the `argv` variable as the name of this array. Since we are allocating space for an array of strings, the total size will be calculated by multiplying the size of character pointers (which is the datatype for strings) by the total number of string tokens.

We therefore get something like this:
```C
argv = malloc(sizeof(char *) * num_tokens);
```

### Store each token in the array
Since we destroyed the `lineptr` if the first set of `strtok` operations, it is no longer available. We therefore have to use the copy we created `lineptr_copy`. You see why it was necessary to create a copy of it?

We will also use a similar process to what we used to count the number of tokens here. However, instead of adding one to the counter each time the loop runs, this time round we will will do two main things. We will first allocate enough space for the specific token then copy the token to the allocated space.

Also, a for loop is preferable for this kind of job as you will see in the code.

> ** Clearing possible confusion**
<br \>Why am I going to allocate another space when we already allocate enough space for `argv` to store the tokens. This is a likely source of confusion for those who do not fully understand the concept of pointers to pointers in C.
<br \><br \> **Let me try and clear out that confusion for you. **
<br \>
The first space that we allocated was the space for the pointer to the string. We are yet to allocate space for the string itself. Remember that we are building an array of strings. hence, we should have a pointer to a number of strings (which in itself is a pointer to characters). <br \>
**Try revising on the pointer to pointer concepts in C programming.** Check out this [thread from Stackoverflow](https://stackoverflow.com/questions/46672153/how-to-allocate-memory-using-a-pointer-to-pointer-in-c)


Now let's see how the code will look like.
```C
token = strtok(lineptr_copy, delim);

        for (i = 0; token != NULL; i++){
            argv[i] = malloc(sizeof(char) * strlen(token));
            strcpy(argv[i], token);

            token = strtok(NULL, delim);
        }
        argv[i] = NULL;
```

After the loop we set the last index of `argv` to NULL to terminate the array of strings.
Here is what our final state of the code looks like:
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


        printf("%s\n", lineptr);

        /* free up allocated memory */ 
        free(lineptr);
    } 


    return (0);
}
```
>**NB:** I introduced a variable `i` for the `for loop` and also removed `(void)argv` because we finally found use for `argv`.

The next step will be to execute the commands in the array of strings (`argv`). That's what we will tackle in the part 3 of this series. But before I end this part, we have to test if the current state of our code works fine.

To help us test the code, let's try printing out the content of `argv` anytime the end user types in something and hit the `Enter` key. We will therefore stop printing just the string they typed in but then print out each token from the string they typed in. This wouldn't be part of the actual shell project but it is good we test out the current state of our code to ensure that we are successfully parsing the string.

We will do that with the help of a `for loop` so let's add a new variable `counter` and implement a `for` loop that prints everything in `argv` except for the terminating NULL byte. The code for that for loop looks like:

```C
/* print the content of argv */
        for (counter = 0; counter<num_tokens-1; counter++){
            printf("%s\n", argv[counter]);
        }
```

We need to free up all the memories we allocated (`argv` and `lineptr_copy`). The final code together with the `for loop` for testing looks like:
```C
#include <stdio.h>
#include <unistd.h>
#include <string.h>
#include <stdlib.h>


int main(void)
{
    char *full_command = NULL, *copy_command = NULL;
    size_t n = 0;
    ssize_t nchars_read; /* number of characters the user types */
    char *token;
    const char *delim = " \n";
    char **argv;
    int i = 0; // x = 0;
    int num_tokens = 0;

    // strcpy(command_copy, full_command);
    /* print a prompt for the user to type something */
    printf("$ ");

    /* get the string that the user types in and pass it to full_command */
    nchars_read = getline(&full_command, &n, stdin);

    /* let's allocate space to store the characters read by getline */
    copy_command = malloc(sizeof(char) * nchars_read);
    
    if (copy_command == NULL){
        perror("tsh: memory allocation error");
        return (-1);
    }

    /* make a copy of the command that was typed */
    strcpy(copy_command, full_command);

    /* check if the getline function failed or reached EOF or user use CTRL + D */
    if (nchars_read == -1){
        printf("Exiting shell....\n");
        return (-1);
    }
    else {
        
        /* split the string (full_command) into an array of words */
        token = strtok(full_command, delim);

        /* allocate space to store the variable arguments but before then determine how many tokens are there*/
        while (token != NULL){
            num_tokens++;
            token = strtok(NULL, delim);
        }
        num_tokens++;
        // printf(">>>>> %d \n", num_tokens);

        /* use malloc to allocate enough space for the pointer to the argument variables */
        argv = malloc(sizeof(char *) * num_tokens);

        token = strtok(copy_command, delim);

        for (i = 0; token != NULL; i++){
            argv[i] = malloc(sizeof(char) * strlen(token));
            strcpy(argv[i], token);

            // printf(">>>>> %s \n", argv[i]);
            token = strtok(NULL, delim);
        }
        argv[i] = NULL;

        /* execute the commands with execve */


        free(argv);
        free(full_command);
        free(copy_command);
    }

    return (0);
}
```

Go ahead, recompile this code and test it out. Do you get something like this?


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1668079276644/0iPpoErs8.png align="left")


Great job. We are finally getting somewhere. Let's continue in the next part.

Check part 3 out with the link below:

%[https://blog.ehoneahobed.com/building-a-simple-shell-in-c-part-3]

## Conclusion
I hope  you are enjoying the series? I haven't had time to cross check the write-up and the codes. I am opened to your suggestions and comments. Let me know your thoughts on it and suggestions that you have in the comment box.

I will also appreciate if you follow [this blog](https://hashnode.com/@ehoneahobed) and subscribe to my [YouTube channel](https://youtube.com/@ehoneahobed?sub_confirmation=1) to show me some love and also to ensure that you constantly get access to the sort of wonderful content that I create on daily basis. If you'd love to chat with me too, then hit ne up in my [DM on Twitter](https://ehoneahobed.com/twitter). I'd love to connect with you.