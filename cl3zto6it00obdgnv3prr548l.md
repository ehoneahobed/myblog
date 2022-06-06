## Write a script that compiles a C file and creates an executable named myApp

The question above doesn't expect you to write a C program but rather a bash script that will be used for compiling various C programs.

This means you will need to know how to write bash scripts to be able to answer this question. If you don't know what a bash script is or how to write one, then check out my previous post on it.

[How to write a script that performs certain commands in Linux](https://medium.com/@ehoneahobed/how-to-write-a-script-that-performs-certain-commands-in-linux-ad4d9681a470)

There are multiple ways to compile a C program into an executable file. One of the most common ways is:
- using the gcc compiler

## How to compile a C program using the gcc compiler
If you are using a Linux distro like ubuntu then you are likely to have the gcc compiler installed on it. Otherwise you can run the command below to install it.

```bash
sudo apt-get install build-essential
```
Once installed, you now have access to the `gcc` command.

To compile a C program with the `gcc` command, you need to pass the file containing your source code as an attribute to the command.

Let's assume that we have a file called `app.c` containing the source code of our C program, the `gcc` command will be:
```
gcc app.c
```
When the above command is run, all the four stages of the C program compilation will be completed and a final output file will be returned.

NB: The 4 stages of the compilation process are: 

1. Preprocessing
2. Actual Compilation
3. Assembly
4. Linking

Hence, the `gcc` command above takes your source code through all these 4 stages and by default gives you an executable file with the name `a.out`.
 
What if you want the executable file to have a specific name?

You can add the option`-o` to the `gcc` command and give the name that you want for the execution file as an attribute.
```
gcc app.c -o myApp
```
The command above means that your source code `app.c` should be compiled into an executable file called `myApp`.
