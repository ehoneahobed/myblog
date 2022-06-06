## Bash Script that converts a number from base 2 to base 10

In one of our Linux assignments as Software Engineering students at ALX, we were to write a script that converts a given value from base 2 to decimal (base 10). 

The specific question we were given stated that the value to be converted was stored as an environment variable. 

Therefore, we will look at how to create a script that converts any number from base 2 to base 10, as well as one that works with the environment variable.

Let's begin by taking a look at how you can do the conversion before we look at how to convert that into an executable script.

## How to convert a number from base 2 to base 10
In the shell, you can use arithmetic expansion to convert any number from one base to the other.

I have already published an article on shell expansion, and I explain what arithmetic expansion is. If you are interested in knowing more about that, then [check out this article](https://medium.com/@ehoneahobed/shell-expansions-in-linux-what-it-means-and-how-to-take-advantage-of-it-41d471cb02dc).

In simple terms, the shell understands certain shortcuts and will always interpret them before executing any commands that have such shortcuts as arguments. This process is known as shell expansion.

For arithmetic expansion, the shortcut is `$(( ))`. Hence, anytime the shell comes across this notation in a command, it is going to arithmetically evaluate the expression within it before passing the outcome to the command.

By default, Shell gives you outputs in base 10. So, to convert a number from one base to the base 10, we pass the number in the arithmetic expansion shortcut and categorically state the base in which it is.

The synthax is as such `$((base_of_interest#number_to_be_converted))`.

So, you need three components for the expression to be evaluated through arithmetic expansion. The first one is the base of interest (2 in our case), followed by # then also followed by the number to be converted.

Let's get practical. Assume we want to convert the number 101101 base two to decimal.

## How to convert 101101 base two to base 10 in Linux

For this example, the expression to be evaluated by arithmetic expansion will look like `$((2#101101))`.

To get the decimal equivalent of this, we have to make the shell display the output of this mathematical expansion. We can achieve that with the help of the echo command. Hence, the shell command will be:

```
echo $((2#101101))
```

Upon executing the above command in the shell terminal, you will get the output 
```
45
``` 
What it means is that the decimal value of 101101 base two is 45.

## Using environment variables in shell commands
Environment variables are a set of values stored within the system and available for use at any point in time within the shell. With each environment variable, there is a variable name and a value assigned to that name.

When using such variables in your commands, all you require is the variable name preceeded by an `$`. For example if we have an environment variable called `BINARY` then we can use this variable in our shell commands like this `$BINARY`.

Let's assume we are supposed to write a shell command to convert the variable above to decimal knowing that the value of this variable is in base 2 (binary).

Our command for the above task will be:
```
echo $((2#$BINARY))
```

## How to convert a shell command into an executable script
There are two main steps to this and I have explained this in a detailed article that I published earlier: [How to write a shell script that performs specific commands](https://medium.com/@ehoneahobed/how-to-write-a-script-that-performs-certain-commands-in-linux-ad4d9681a470).

In summary, you need to introduce your script with the shebang declaration and then give your script an execution permission after saving it.

The shebang declaration to be used is `#!/bin/bash` and you give it execution permission by running the command `chmod +x name_of_script`

Putting it altogether:

a. A script (let's call the script binary_converter) that converts 101101 base two to base ten will look like 
```
#!/bin/bash
echo $((2#101101))
```
Then save this file with the name `binary_converter`. You can then go on to grant the execution permission like such:
```
chmod +x binary_converter
```
b. A script that converts an environment variable (say $BINARY) from base two to base ten will look like:
```
#!/bin/bash
echo $((2#$BINARY))
```

Save the script and grant it the execution permission as explained earlier.

### Conclusion
In this article, you have learned how to convert any number from binary (base 2) to decimal (base 10). This can as well be applied to other bases, go ahead and give that a try.

I will love some feedback from you so do leave a comment for me. Also, I would love to connect with you if you read this article, so kindly [DM on Twitter](https://twitter.com/ehoneahobed) and let’s have a good chat.