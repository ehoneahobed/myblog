# Building a simple shell in C - Part 1

One of the projects I previously worked on as part of my software engineering training at ALX Arica was building a simple shell that mimics the Bash shell but with limited features. 

Recently, I have had a few people reach out to ask specific questions about the project, and others want me to organize a tutorial session on it.

Thinking about it, I realized that I had forgotten most of the things because I haven't been coding in C for a while now. As a result, I've decided to create a tutorial series on the project to help me revise the concepts and to assist anyone who needs it. I may eventually record a YouTube video on this, though.

I will break the complex project into simpler parts so that all readers will understand and be able to build their own simple shell.

As such, my goal for this first part is to show you how to get started with the project, and at the end of this part, you should have a basic shell that prints a prompt for the end user to type in something and prints out exactly what the user typed on the next line.

This is thus in two parts:
- Printing the prompt
- Reading and printing what the end user types out.

I held a brainstorming session with my team and I explained the workings of the shell. Hence, if you don't fully understand how the Bash shell works then you will want to begin by watching this video to grasp the concept so you can easily follow along with this series.

%[https://youtu.be/4jYFqFsu03A]

But before we implement these, let's first set up the boilerplate code for a C program.

## Boilerplate code for a C program
To get started, we need to include some header files which will then allow us to use some of the native functions available in C. One example of such is the `<stdio.h>` which will enable us use the `printf()` function to print information to the terminal.

Because this is going to eventually become a big project, I would want to separate the header files from my main files. I will therefore start by creating a directory (`Eshell`) for my project and create two files (`main.c`, `main.h`) inside that directory.

### Creating directory and files
```Bash
>>> mkdir Eshell
>>> cd Eshell
>>> touch main.c main.h
```
You can then go ahead and open these files in any text editor of your choice to continue with the rest of the project. In my case, I will be using VS code and the shortcut to open the current directory in VS code directly from my terminal is to run the code `code .`

```Bash
>>> mkdir Eshell
>>> cd Eshell
>>> touch main.c main.h
>>> code .
```
This launches VS Code immediately, and as you can see below, I have both files in there.
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1667983089716/BVyohWa2y.png align="left")

Let's proceed to write some code in the files.

### Add header files to main.h file
```C
#include <stdio.h>
#include <stdlib.h>
```

### Add boilerplate code to main.c file
```C
#include "main.h"

int main(int ac, char **argv){

   return (0);
}
```
Now that we have the boilerplate for a C program rightly set up, let's proceed to printing a prompt for the end user.

## Printing a prompt
With the help of the `printf` function, we can print out any symbol that we want to use as our prompt. In this case, I choose to go with `(Eshell) $ `. This means that, this prompt is going to show up anytime we want a user to type in something.

Let's add it to our `main.c` file.

```C
#include "main.h"

int main(int ac, char **argv){
  char *prompt = "(Eshell) $ ";

  printf("%s", prompt);
  return (0);
}
```
After printing the prompt, we need to get the line (as in get everything that the user types).

## Reading and printing what the end user types out
To be able to get what the user types, we need to make use of a standard function called `getline`. If this is the first time hearing about it or you know it but what to check out how it is used, you can run the command `man 3 getline` on any linux terminal to get the details about it.


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1667984610620/jQtWE8A9_.png align="left")

From the image above, you can see that the prototype for that function is:
`ssize_t getline(char **lineptr, size_t *n, FILE *stream)`. To be able to have access to the prototype, we need to add the header file `stdio.h` which we have already done.

```C
#include <stdio.h>
#include <stdlib.h>

```

To be able to use this `getline` function in our `main.c` we will need to create some variables with the respective data types according to the given prototype.

- `char *lineptr` to store the address of the buffer holding whatever was typed.
- `size_t n` to store the allocated size in bytes.
- The `stream` represents the source from which we want the function to get the data from. In our case, that will be the standard input (i.e. whatever is typed from the keyboard). We will therefore use `stdin` as the stream.

NB: The `getline` function allocates memory dynamically and hence we would have to free the memory by ourselves whether the function execution succeeds or fails.

```C
#include "main.h"

int main(int ac, char **argv){
  char *prompt = "(Eshell) $ ";
  char *lineptr;
  size_t n = 0; 

  printf("%s", prompt);
  getline(&lineptr, &n, stdin);

  free(lineptr);
  return (0);
}
```

NB: Remember that I used `&` when passing the variables to the `getline` function because I was [passing those variables by reference](https://www.tutorialspoint.com/cprogramming/c_function_call_by_reference.htm).

### Printing out what was typed
What happened with the `getline` is that it copied what the person typed into our `lineptr` variable. Therefore to print out what was type, we just need to print what `lineptr` contains (technically, what it is pointing to).

```C
#include "main.h"

int main(int ac, char **argv){
  char *prompt = "(Eshell) $ ";
  char *lineptr;
  size_t n = 0; 

  printf("%s", prompt);
  getline(&lineptr, &n, stdin);
  printf("%s\n", lineptr);

  free(lineptr);
  return (0);
}
```

Now our basic shell is ready and we need to compile it and test it out.

## Compiling and Testing out the basic shell
We will compile with `gcc` and some predefined flags. The executable file will be called `eshell`. So go ahead and use the command below to compile your code.
`gcc -Wall -Wextra -Werror -pedantic main.c -o eshell`

But because of the flags we are using, we can't leave any of the variables used. For that matter we have to declared both the `ac` and `argv` variables as void variables for the time being.

Make the following updates to your code before you compile the code.
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
Open your terminal and run the code. In VS code, you can open a terminal with the shortcut ```CTRL + ` ``` or ```Ctrl+Shift+` ``` to open up a new terminal.

After your terminal is opened, type in the code for compilation. 
`gcc -Wall -Wextra -Werror -pedantic main.c -o eshell`


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1667987282959/R_MsaM1Im.png align="left")

It's time to run your executable to see what you get. You expect that the objective for this part be achieved. That is; 
Your `eshell` should give you a prompt and display whatever you type in it right after clicking the enter key.

To run the executable, you need to use the terminal and issue the command below
```Bash
./eshell
```

This is what I got when I run mine.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1667987524441/Lu3rWuixf.png align="left")

Well done. We will continue in part 2 of the series.

**Part 2 available now:**

%[https://blog.ehoneahobed.com/building-a-simple-shell-in-c-part-2]

## Conclusion
I hope you enjoyed reading this as much as I enjoyed writing it. I look forward to continuing and showing every aspect of building your own shell. As I mentioned earlier, I may also record YouTube videos explaining these concepts.

So, in order not to miss out on any of the videos, subscribe to my [YouTube channel](https://youtube.com/@ehoneahobed?sub_confirmation=1).

Also, if you like the content I am putting out and would like to support me, then follow [this blog](https://hashnode.com/@ehoneahobed) and follow me on [Twitter](https://ehoneahobed.com/twitter) where I document most of the things I am learning and projects I am working on.