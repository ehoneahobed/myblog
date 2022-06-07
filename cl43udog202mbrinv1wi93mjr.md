## Write a bash script to count the number of directories

If you have a given directory that contains several other subdirectories, how will you know how many subdirectories there are in total?

Hence, for the task, you have to write a bash command that will count all the subdirectories and then create a bash script out of that command.

I have already tackled how to create a bash script to perform a given command and, for that matter, I will only focus on writing the command in this case.

You can check out my previous post: [How to create a bash script to perform a given task](https://medium.com/@ehoneahobed/how-to-write-a-script-that-performs-certain-commands-in-linux-ad4d9681a470) here. 

## Bash command to count the number of directories
In order to achieve this, we will need to make use of two different Linux commands. One will have to execute and afterwards pass it outcome as the input (or attribute) for the second command.

We therefore need to know about these two commands and how to use them. But before them, I want us to see how we can pass the output of the first command as input for the second command.

There is also concept called pipping (involves using pipelines `|`) in between two or more commands. Anytime a pipe `|` is introduced between two commands, the output of the first command is passed as input to the second command.

```
first_command | second_command
```

The two commands that we are going to use are:

- `find` command
- `wc` (word count) command

We are going to use the `find` command to search (find) and list all the subdirectories within the current directory.

We will then pass on that list to the `wc` command to count the total number of directories present.

These two commands can do a lot more things than what we want them to do for us now. For that matter, we need to provide some options for each command in order to get exactly what we want.

## Using the `find` command to list all subdirectories in current directory

For instance, the `find` command will search and list any file, both directories and non-directories alike. So, we need to restrict the search to only directories.

Also, we need to tell the `file` command where it needs to search and to what extent it needs to search. All these things can be achieved with various options. Let's take a look at the options to use.

### Option to check for only directories
In order to restrict the `find` command to only directories, we use the `-type` option. This option will take the attribute `d` to indicate directories. So, we will get something like:
```bash
find -type d
```

### Option to set the level of the search
Now, the question is, how deep should the search be. From the main question, we need to count all directories and their respective subdirectories in the current directory.

For that matter, the depth should start from the current directory to as deep as it gets.

In terms of depths, we can say that you should start at a minimum depth of 1 (that's referring to any directory present in the current directory) but we won't set a maximum since we want it to go as deep as it can.

The option to use is `-mindepth` and give the number as the attribute. In this case, the attribute will be 1. The command will then look like:

```bash
find -mindepth 1
```
> NB: We could have set a `-maxdepth` if the question demanded

Let's then go ahead and put the commands together. We get:

```bash
find -mindepth 1 -type d
```

The above code will list all the directories and subdirectories present in the current directory.

## Using `wc` to count the number of directories
`wc` as a command can be used to count a lot of things include:

- Number of lines
- Number of words
- Number of characters

With this task, we want it to print the total number of lines that were printed out by the `find` command.

To get the `wc` command to count number of lines, we need to provide the option `-l`. The command will therefore be:
```bash
wc -l
```

## Solution to the question
We now need to put both of the commands together with the help of a pipe `|`.
Our final command for solving this question is:
```bash
find -mindepth 1 -type d | wc -l
```
 
### Conclusion
I hope you enjoyed reading this and it made you understand how to solve a problem like this. I would like to hear back from you. Is there anything I missed, or explained wrongly, or something you want me to elaborate more on?

Share with me what you also think. Mind you, I am also learning and your feedback will be valuable to me.

Thanks for reading and I would love to connect personally with you. If you are on Twitter, then you can [send me a DM](https://twitter.com/ehoneahobed) and let's have a good chat.