## How to connect your computer to GitHub with SSH

Once you start using git with github on your computer, you are likely to look for an easy way to push your codes from your local repository to your remote repository (github in this case).

To enable this, you need to establish a connection between your computer and the GitHub servers. There are two common ways to establish this connection. These are:
- Using HTTPS
- Using SSH

In this article, I will share with you how you can establish that connection using the secure shell (SSH) protocol.

Once, the SSH connection is established between your GitHub account and your computer, you can clone any repo and push to it without needing a password or personal access token.

To establish the connection, you need to generate SSH keys (both private and public keys) on your computer and then share the public key with GitHub. 

## How to generate SSH keys on your computer
Open any terminal of your choice (eg: git bash) and type the command below:
```bash
$ ssh-keygen -o -t rsa -C "sample@ehoneahobed.com"
```
Remember to replace `sample@ehoneahobed.com` with your own email.

You will get an output like below:
```xml
$ ssh-keygen -o -t rsa -C "sample@ehoneahobed.com"
Generating public/private rsa key pair.
Enter file in which to save the key (/c/Users/ehone/.ssh/id_rsa):
```
Pay attention to what is in the parenthesis of the last line. That is the default location of the key and you are being asked to enter a specific file or directory where you want to save the ssh keys generated.

I prefer you go with the default location, so just click on the enter key to continue.

The next two prompts will be asking you to enter a passphrase and confirm it, but you can ignore that by clicking the enter key. 
```xml
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
```
After clicking enter, your key is generated and you get a message like below
```xml
Your identification has been saved in /c/Users/ehone/.ssh/id_rsa
Your public key has been saved in /c/Users/ehone/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:V7dW7zlyUlG+mJ+n1AP97kMY775S3GypJ8d/IVCVj9M sample@ehoneahobed.com
The key's randomart image is:
+---[RSA 3072]----+
|              ..o|
|             . o.|
|            o .++|
|           o o*oE|
|        S . .+B*+|
|         .   ++XB|
|             oOO*|
|             =+O=|
|              B+O|
+----[SHA256]-----+
```
Now let's locate the file containing the public key so we can copy it. You can use the command below to list the files present in `.ssh` directory.
```bash
$ ls ~/.ssh
```

Outcome of the above command is a list of all the files that are available in that directory as shown below.

```xml
id_rsa  id_rsa.pub  known_hosts  known_hosts.old
```

The public key is contained in the file with the `.pub` extension. To open it in your terminal, you can run the command below:
```bash
$ cat ~/.ssh/id_rsa.pub
```
This command shows you the ssh public key which will begin with `ssh-rsa` and end with the email address you used.

#### NOTE:
Another way of getting the content of the public key after generating it will be to open the exact directory in which it was created and open the `id_rsa.pub` file with any text editor.
The directory was the default directory that I pointed out to you earlier (in my case: 
 **/c/Users/ehone/.ssh/id_rsa**). It may however, differ if you changed it.

Copy the public key and head over to github.

## How to add your Public SSH key to GitHub
- Go to https://github.com and sign into your GitHub account
- Navigate to your account settings. If you don't know where to find it, click on your profile picture and check the dropdown menu for `settings`
- On the left sidebar, click on SSH and GPG keys link
- Click on add new SSH key button
- Paste the key you copied into the textbox for "key"
- Give your key a title
- Save key
- You will be asked to confirm your github account password before the key is successfully added.

Below is a pictorial workflow that will guide you to add a public SSH key to your github account.

<iframe src="https://scribehow.com/embed/Github_Workflow__4aKy3Ik3TN6ciaSmhL5_9Q" width="640" height="640" allowfullscreen frameborder="0"></iframe>

You can download the [workflow with the by clicking here](https://drive.google.com/file/d/112yZH0Zf9Ic__97g_wY0PFzDO-kMWv_X/view?usp=sharing).

Congratulations, you have successfully connected your computer to the Github server. You can now clone any of your repos and also push to them without worrying about passwords or personal access tokens.

## How to clone a GitHub repo after SSH connection
- Visit your github account and locate the repo that you want to clone
- Click on the green "Code" button
- Look for SSH (found between HTTPS and Github CLI) and click on it
- You can then copy the link provided. The link looks like
```
git@github.com:ehoneahobed/name_of_repo.git
```
Now, go back to your terminal and clone the repo using the `git clone` command.
```bash
git clone git@github.com:ehoneahobed/name_of_repo.git
```

After successfully cloning your repo, you can make all the changes you want. Remember to stage and commit the changes before pushing them to the remote repo. You may be asked to set an upstream branch.

## Conclusion
This was something I really struggled when I began using git and github and I am aware a lot of other people struggle with it as well. That was my motivation for writing this post. I hope it clarified the process for.

If you have any questions, you can ask in the comments or reach out to me on [Twitter](https://twitter.com/ehoneahobed)if you want to connect with me.