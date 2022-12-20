# Step-by-Step Guide to Installing and Configuring HAProxy on Ubuntu

My first encounter with a load balancer was when I was studying for my AWS practitioner certification exams. At the time, I was really finding it difficult to grasp the concept. But with time, I came to understand its importance.

Just today, as part of our project for the day (ALX Software Engineering Program), we were given three different servers and asked to configure one of them to be a load balancer that shared the load between the other two servers.

I am therefore going to give you a step-by-step guide on how I installed and configured **HAProxy**, which is the load balancer software we used.

Unlike the other services that I have ever installed on a server, HAProxy was a bit different. It required me to know the version of Ubuntu I was using on the server. So, let's take a look at how I went about it.

Below is a summary of the steps that I followed:

*   Connect to my server through SSH
    
*   Check the version of Ubuntu that was running on my server
    
*   Get the specific HAProxy package for your version of Ubuntu
    
*   Configure HAProxy to share requests between two servers
    
*   Restart HAProxy
    

## Connecting to Ubuntu Server using SSH

There are a couple of ways to connect to a remote Ubuntu server. Using SSH is a common and very secure way. To get access to the server, we need to connect via SSH.

Since you are using SSH, it is required that the local machine that you are using to access the remote server have a private key that matches a public key on the remote server.

If that is so, you can easily connect to the remote server by running the command below on your terminal.

```bash
ssh username@ip_address_of_remote_server
```

Where `ip_address_of_remote_server` is replaced with the actual IP Address of your server and `username` is replaced with your username or and authorized username on the remote server.

If it doesn't work or you get a permission denied error, then you may have to explicitly provide the path to your identity file (your private key). You can do this with the help of the `-i` option.

If your private key is stored in a file called `id_rsa` which is located in the `~/.ssh/` directory, then your command for connecting to the server becomes:

```bash
ssh -i ~/.ssh/id_rsa username@ip_address_of_remote_server
```

## Check the version of Ubuntu that was running on my server

Once, you have successfully connected to the remote Ubuntu server, you need to check the version of Ubuntu installed on it. To find it, run the command below:

```bash
lsb_release -a
```

In my case, my remote server was running **Ubuntu version 20.04**. It may be different for yours, but for the rest of this post, I will be using this version.

This means that anywhere you see me use this version, you would have to replace it with your version when trying to implement it at your end.

## Get the specific HAProxy package for your version of Ubuntu

To get the specific HAProxy package as well as details on its installation for your version of Ubuntu, you need to visit the [Debian/Ubuntu HAProxy packages](https://haproxy.debian.net/) website.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1671491722574/LF0H-91y-.png align="center")

Just as you can see from the image above, you will need to provide three different details. They are:

*   The operating system you are running on your server (Ubuntu in our case)
    
*   The version of Ubuntu you are running (20.04 in my case)
    

*   The version of HAProxy you want to install
    

The image below shows the values I provided for my use case.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1671492005500/D0Xiuzc8n.png align="center")

After providing these details, you get the instructions on how to install HAProxy on your server.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1671492060169/y7gv21g79.png align="center")

The three commands provided are to be run in that order.

```bash
apt-get install --no-install-recommends software-properties-common
add-apt-repository ppa:vbernat/haproxy-2.6
apt-get install haproxy=2.6.\*
```

After you have successfully run all the above commands, you will now have HAProxy installed on your server.

## Configure HAProxy to share requests between two servers

To configure the HAProxy, you will need to identify the algorithm you are going to use for load balancing and also the IP addresses of the servers you will be distributing the load amongst.

Let's use hypothetical values for these in order to make it more practical. Here are the details:

|  | Sample Values |  |
| --- | --- | --- |
| Algorithm | **roundrobin** |  |
| Server1 | name: web-01 | IP-address: 100.25.10.201 |
| Server2 | name: web-02 | IP-address: 100.25.10.202 |
| Port | 80 |  |

We will need to configure both the frontend and the backend for the HAProxy load balancer. A sample configuration will look like this:

```bash
frontend  ehoneah-frontend
        bind *:80
        mode http
        default_backend ehoneah-backend
backend ehoneah-backend
        balance roundrobin
        server web-01 100.25.10.201:80 check
        server web-02 100.25.10.202:80 check
```

We need to append this to the HAProxy configuration file. The configuration file is located in `/etc/haproxy/haproxy.cfg`. You can therefore open this file with root privileges and append the above configurations to whatever is in it.

```bash
sudo vim /etc/haproxy/haproxy.cfg
```

It is, however, advisable to make a copy of the original file before making changes to it so that you can always have a backup to rely on. To make a copy of it, you can run the command below:

```bash
sudo cp -a /etc/haproxy/haproxy.cfg{,.original_copy}
```

The command above will copy the file `/etc/haproxy/haproxy.cfg` to `/etc/haproxy/haproxy.cfg.original_copy`

Now, you can peacefully go ahead and update the configure file by appending the additional configurations for both the frontend and backend as I illustrated earlier.

The final thing you want to do is to enable HAProxy to be started by the init script. You do this by appending the command `ENABLED=1` to the file `/etc/default/haproxy`.

You can do this by opening the file in a text editor like `vim` and appending the command to the content of the file. You can also do it directly by running the command below:

```bash
echo "ENABLED=1" | sudo tee -a /etc/default/haproxy
```

## Restart HAProxy

Finally, you need to restart HAProxy for the new configurations to take effect. You can restart it with the command below:

```bash
sudo service haproxy restart
```

## Conclusion

These few weeks have been really great. Working with servers and learning a lot of new things. This is one of the many things that I have learned how to do and look forward to sharing more of the things that we are learning with you.

If you enjoy this content and want to see more content like this, subscribe to this [blog](https://hashnode.com/@ehoneahobed) and also you can show me some support by subscribing to my [YouTube channel](https://youtube.com/@ehoneahobed?sub_confirmation=1) as well.

If you love to connect with me personally, then my [Twitter DMs](https://ehoneahobed.com/twitter) are always open, just send me a message and let's chat.