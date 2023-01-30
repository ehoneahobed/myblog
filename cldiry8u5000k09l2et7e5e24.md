# How to securely transfer files to a remote server and automate it with a bash script

You may sometimes want to upload a file on your computer to a remote server. There are a couple of ways that you can do that but one of the common and secure ways of doing it is by using the `scp` command.

In this post, we will discuss how to use the `scp` command to securely transfer a file to a remote server. We will then go a step further to automate the process by writing out a simple bash script for it.

Let's get started by looking at how the `scp` command works.

If you love learning by watching videos, then check the associated [video](https://youtu.be/HBJOkOF_Ydo) for this tutorial:

%[https://youtu.be/HBJOkOF_Ydo] 

## How does the `scp` command work?

Do you know of the `cp` command used on linux machines? The `cp` command is used to copy from one location to another.

The `scp` command which stands for `secure copy` is similar to the `cp` command except that it does the copying securely and remotely.

The `scp` command is used to transfer files between computers over a network. It uses the SSH (Secure Shell) protocol to securely transfer the files and provides the same level of security as the `ssh` command.

Anytime you run the `scp` command, it establishes a secured connection with the remote server through the SSH protocol. Once this connection is established, all the provided files are transferred over the network to the specified destination on the remote server.

> Note that you can use `scp` to copy files from a remote server to your local machine or to transfer files from your local machine to a remote server.

## Syntax of scp for file transfer

```bash
scp [options] [source] [destination]
```

1. `scp` as you know is the name of the command
    
2. `[options]` refers to some options that you can provide that modify the behavior of the `scp` command. This is optional. The `scp` command supports several options that can be used to modify the behavior of the command, such as specifying a different port number or enabling verbose mode to see detailed information about the transfer.
    
3. `[source]` refers to a file on your local machine or a file on a remote server
    
4. `[destination]` refers to either a local directory or a directory on a remote server.
    

## How to transfer a file to a remote server

For example, to copy a file named "ehoneah.txt" from your local machine to a remote server, you would use the following command:

```bash
scp ehoneah.txt username@remote_server_ip:/path_to_remote_destination
```

Where `username` refers to the username that you use on the remote server, `remote_server_ip` refers to the IP address of the remote server, and `path_to_remote_destination` refers to the actual path to the directory on the remote server where you want to store the file.

## How to copy a file from the remote server to your local machine

If you want to any file from a remote server to your local machine, then you have to use the syntax below:

```bash
scp username@remote_server_ip:path_to_remote_file /path_to_local_destination
```

The difference between this one and the previous one is that your remote server becomes the source here, whereas it was the destination in the previous one.

#### Important Note:

By default, `scp` uses the same authentication methods as `ssh`, such as password-based authentication and public key authentication. So, you'll need to have ssh access to the remote server to execute the scp command.

## Bash script to automate the uploading of files to a remote server

To help us automate the process of transferring files from a local machine to a remote machine, we will write a bash script for it.

This bash script should take about 4 different arguments.

* The path to the file to be transferred
    
* The IP of the server we want to transfer the file to
    
* The username `scp` connects with
    
* The path to the SSH private key that `scp` uses
    

Note that the last argument may be necessary if your private key is not stored in the default location.

Since the last argument is optional, we would have to make use of conditional statements in our bash script to determine whether it was provided or not. We will also check if the number of arguments provided is less than 3. If less than three then we can't proceed, hence we will throw an error at the user.

```bash
#!/usr/bin/env bash
if [ "$#" -lt 3 ]; then
	echo "Sorry, you are using the script wrongly. The right usage should follow this pattern: ./scriptname PATH_TO_FILE IP USERNAME PATH_TO_SSH_KEY"
elif [ "$#" -lt 4 ]; then
	scp "$1" "$3@$2":~/
else
	scp -i "$4"  "$1" "$3@$2":~/
fi
```

This script is a simple example of how the `scp` command can be used in a Bash script. It allows you to transfer a file to a remote server with a single command, and also allows you to specify a path to the private key if needed.

This script uses the `scp` command to transfer a file from a client to a server. The script is written in Bash and can be executed by running `bash` [`scriptname`](http://scriptname.sh) or `./scriptname` after making the file executable.

### Here is the explanation of the Bash script above:

1. `#!/usr/bin/env bash` - This is the shebang line. It tells the operating system to execute the script using the Bash interpreter.
    
2. `if [ "$#" -lt 3 ]; then` - This is an if statement that checks if the number of command-line arguments passed to the script is less than 3. `$#` is a special variable in Bash that holds the number of arguments passed to the script. The `[ "$#" -lt 3 ]` part is a test that returns true if the number of arguments is less than 3.
    
3. `echo "Sorry, you are using the script wrongly. The right usage should follow this pattern: ./scriptname PATH_TO_FILE IP USERNAME PATH_TO_SSH_KEY"` - If the number of arguments is less than 3, the script will display a message indicating the correct usage of the script.
    
4. `elif [ "$#" -lt 4 ]; then` - This is another if statement that checks if the number of command-line arguments passed to the script is less than 4. It's an "elif" statement, which means it's executed only if the preceding "if" statement is false.
    
5. `scp "$1" "$3@$2":~/` - If the number of arguments passed to the script is 3, this line will use the `scp` command to transfer the file specified by the first argument, `$1`, to the remote server specified by the second argument, `$2`, and the user specified by the third argument, `$3`. The `:~/` at the end of the command specifies that the file should be copied to the home directory of the remote user.
    
6. `else` - This line is the beginning of an else statement. This block of code will be executed only if the preceding "if" and "elif" statements are false.
    
7. `scp -i "$4" "$1" "$3@$2":~/` - If the number of arguments passed to the script is 4, this line will use the `scp` command with the `-i` option to specify the path to the private key file, specified by the fourth argument, `$4`, to transfer the file specified by the first argument, `$1`, to the remote server specified by the second argument, `$2`, and the user specified by the third argument, `$3`. The `:~/` at the end of the command specifies that the file should be copied to the home directory of the remote user.
    
8. `fi` - This line ends the if-else statement.
    

In case, you didn't want to save the file to the home directory but a different one, say, the downloads directory, your script will look like this:

```bash
#!/usr/bin/env bash
if [ "$#" -lt 3 ]; then
	echo "Sorry, you are using the script wrongly. The right usage should follow this pattern: ./scriptname PATH_TO_FILE IP USERNAME PATH_TO_SSH_KEY"
elif [ "$#" -lt 4 ]; then
	scp "$1" "$3@$2":~/downloads/
else
	scp -i "$4"  "$1" "$3@$2":~/downloads/
fi
```

## Conclusion

I hope you enjoyed this post and have gotten a better understanding of it. I look forward to writing more on various DevOps concepts. If you are interested in such content or the other software engineering topics that I write about, go ahead and follow this [blog](https://hashnode.com/@ehoneahobed).

If you would love to connect with me, then send me a [Twitter DM](https://ehoneahobed.com/twitter), and let's have a chat.

You can also support me by subscribing to my [YouTube channel](https://youtube.com/@ehoneahobed) where I create similar content but in video format.

Thanks for reading and supporting me.