## Write a script that compiles a C file but does not link

In my previous post, I wrote on how you can [write a script that preprocesses a C source code and produce the output into a new file](https://blog.ehoneahobed.com/script-that-runs-a-c-file-through-the-preprocessor).

In that article I described the four main stages of C program compilation;


1. Preprocessing
2. Actual compilation
3. Assembly
4. Linking

The import of this task is to focus on just the first three stages and returning a result for the third stage. 

Thus, the script you write as a solution to this problem will have to take the C source code through preprocessing, followed by the actual compilation stage and finally the assemby stage. 

Hence, the output that will be returned is the outcome of the assembly process. Let's take a practical example to discuss how to go about this.

A practical example:
```bash
Write a script that compiles a C file but does not link.

- The C file name will be saved in the variable $MYFILE
- The output file should be named the same as the C file, but with the extension .o instead of .c.
- Example: if the C file is test.c, the output file should be test.o
```

## What does the question actually mean?
It is important for you to know that this question is not demanding that you write a C program.

Instead, it is asking that you create a bash script that will be used for the compilation of a given C program and give the output of the assembly process.

However, to be able to write such a bash script, you need to understand how you can compile a C program and convert that step/command into a bash script.

## How do I get my C program to be compiled?
There are a number of C compilers that you can use. One of the most common compilers available in almost every Linux distribution is the GNU Compiler Collection (GCC).

With the GCC, you can use `gcc` command in your terminal to compile your C program.

This command can, however, take up different options. The options provided will determine which stages of the compilation your source code will be taken through and the kind of output file you will get.

## What `gcc` option is used for the first three stages?
The option to get the output of the assembly stage (including preprocessing, and compilation) is `-c`.

This means that if you want to do all the first three stages of the compilation, then you have to run the command below;

```bash
gcc -c name_of_source_file
```
  
where `name_of_source_file` is the name of the file containing your source code.

You may provide the name you want to give the output file as an attribute to the `gcc` command with the help of the option `-o`. That will look like;

```bash
gcc -c name_of_source_file -o name_of_output_file
```

The `gcc -c` command gives you an output file with the `.o` extension. Also, if you don't provide the name of the final output file, then it automatically uses the same name as the source code file.

## Solution to the practical question
The question was
```bash
Write a script that compiles a C file but does not link.

- The C file name will be saved in the variable $MYFILE
- The output file should be named the same as the C file, but with the extension .o instead of .c.
- Example: if the C file is test.c, the output file should be test.o
```

If you don't know how to write a bash script then check out my previous post on [how to do that](https://medium.com/@ehoneahobed/how-to-write-a-script-that-performs-certain-commands-in-linux-ad4d9681a470).

It is also worth noting that the C file which is to be our source code has been saved into a variable called $MYFILE. This means that you should replace the name of the source code file in your command with the variable $MYFILE.

The solution thus will be like:

```bash
#!/bin/bash
gcc -c $MYFILE
```

This means that the script above will compile any source code stored to the variable `$MYFILE` and give the output in assembler language with the extension `.o`.

### Conclusion
I hope you enjoyed reading this and it made you understand how to solve a problem like this. I would like to hear back from you, is there anything I missed, or explained wrongly or something you want me to elaborate more on?

Share with me what you also think, mind you I am also learning and your feedback will be valuable to me.

Thanks for reading and I will love to connect personally with you. If you are on Twitter then you can [send me a DM](https://twitter.com/ehoneahobed) and let's have a good chat.