---
title: "Quickly Find Your Ubuntu Version with Terminal: Easy Steps"
datePublished: Wed Apr 12 2023 12:00:39 GMT+0000 (Coordinated Universal Time)
cuid: clgdn3y8u027pp2nv9l7v8og4
slug: quickly-find-your-ubuntu-version-with-terminal-easy-steps
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1681244390205/9f914dd3-8ae8-4371-8bd6-23ef02717a7e.png
tags: ubuntu, linux, linux-for-beginners, ubuntu-server

---

If you are an Ubuntu user and want to check the version of Ubuntu you are using, you can easily do so using the terminal. In this article, we will discuss how to check the Ubuntu version using the terminal.

Ubuntu is updated regularly, and each new release comes with updated software packages and improved features. Therefore, it is essential to know which version of Ubuntu you are using so that you can check if any updates are available and install them. Here's how you can check the Ubuntu version using the terminal.

## Step 1: Open the Terminal

To open the terminal, press `Ctrl+Alt+T` on your keyboard. Alternatively, you can click on the terminal icon in the applications menu.

## Step 2: Type the lsb\_release Command

In the terminal window, type the following command and press Enter:

```bash
lsb_release -a
```

This command will display the Ubuntu version you are currently using, along with other system information. The output will look something like this:

```yaml
No LSB modules are available.
Distributor ID: Ubuntu
Description:    Ubuntu 22.04.1 LTS
Release:        22.04
Codename:       jammy
```

The output shows that the user is running Ubuntu 22.04.1 LTS, which is the latest version of Ubuntu as of April 2023.

If you only want to see the Ubuntu version number, you can use the `-r` option with the lsb\_release command. Type the following command in the terminal:

```bash
lsb_release -r
```

The output will show only the Ubuntu version number, like this:

```yaml
Release:        22.04
```

This output confirms that the user is using Ubuntu 20.04.

## Conclusion

In conclusion, checking the Ubuntu version using the terminal is a simple and easy process. With just one command, you can find out which version of Ubuntu you are using and whether any updates are available.

Knowing the Ubuntu version is essential for keeping your system up-to-date and ensuring compatibility with software packages. So, the next time you need to check your Ubuntu version, just open the terminal and run the `lsb_release` command.

PS: I love geeking out on Twitter about software engineering-related things, you can connect with me on Twitter(@[ehoneahobed](https://ehoneahobed.com/twitter)) and send me a DM if you want us to chat.