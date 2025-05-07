# Generate SSH Key on Windows with Windows CMD/PowerShell | GridPane

# Generate SSH Key on Windows with Windows CMD/PowerShell

 

4 min read 

## Index

To get the most out of the GridPane platform, you’ll often find the need to use SSH to log into your server and use our GPCLI (GridPane Command Line Interface) commands. GPCLI a powerful set of tools that allow you to customize not only your server but your WordPress installations as well.

For security reasons, SSH access is only available with the use of an SSH key and is restricted to the root user.

WARNING: The Peter Parker Principle applies here!

With great power comes great responsibility.

Not familiar with Spider-Man? In simple terms – the root user can do anything including deleting and breaking everything. Just a few bad keystrokes and everything can go away. Be careful with the commands you use and never share your Private SSH Key with anyone!

 

## Step 1: Check if ssh client is installed

Make sure you have the latest updates of Windows if that is not possible, then at least you should have the  Windows 10 Fall 2018 build update. From this update, Windows 10 now comes with a built-in ssh client!

To check if the client is working, fire up a Powershell or CMD window and type in this
```
ssh
```

If the client is installed, you should get the following reply:

![mceclip0.png](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='0'%20height='0'%20viewBox='0%200%200%200'%3E%3C/svg%3E)

## Step 2: Create Your SSH Key Pair

Type the following command at the prompt then press enter.

```
ssh-keygen -b 4096
```

When prompted for the file in which to save the key, press enter. The default location will be created.

Keep default values and no need for a pass phrase.

Congratulations! You now have an SSH key. The whole process will look like this:

What does all this mean?

The key generating process has created two files.

id_rsa (this is your private key, do not lose or give this to anybody!)

id_rsa.pub (this is your public key, you copy this to servers or give to others to place onto servers for you to authenticate against using your private key)

These keys are store by default in:

```
C:\Users\WINUSER/.ssh/id_rsa.pub
```

The path might be different but you will always see it when generating the SSH Key, and, it may actually display as below depending on whether your system displays file extensions or not:

```
C:\Users\WINUSER/.ssh/id_rsa
```

back to top ▲

 

## Step 3: Copy Your Public Key To Your Clipboard

We will use our good old notepad to get the contents of our public SSH key

You will need to run the following command. Remember to replace WINUSER with your own user

```
notepad C:\Users\WINUSER/.ssh/id_rsa.pub
```

The output will look similar to this

Now type CTRL+A then CTRL+C to copy the contents from notepad

back to top ▲

 

## Step 4: Add Your Public Key To Your GridPane Settings

Highlight the output of the previous command and press enter. This copies the data to your clipboard. You may find it useful to paste this into a Notepad document while you log into your GridPane account.

Once logged in, click on your name to display the dropdown menu.

If you do this all correctly, your new key will appear below in the Active SSH Keys list.

back to top ▲

 

## Step 5: Push Your Public Key To Your Server

Now push the key to the public server as described  in this articleAdd/Remove an SSH Key to/from an Active GridPane Server

back to top ▲

 

## Step 6: Connect To Your Server

To connect to the server, type the following in the terminal:

```
ssh [root@ipaddress](https://gridpane.com/cdn-cgi/l/email-protection#61130e0e1521081100050513041212)
```

For my example, this is

```
ssh [[email protected]](https://gridpane.com/cdn-cgi/l/email-protection#3e4c51514a7e0f0b07100c0e0d100f0609100f06)
```

Wait, root? But I did not name my key root! That doesn’t matter. Every key, regardless of name, that is added to your GridPane Active SSH Keys is a root key.

If this is your first time connecting to this server, you will be asked if you want to continue connecting and add this IP address to your list of known hosts. Type yes.

If the private key on your machine matches the public key on the server, you will be authenticated and connect to the server.

The whole process looks like this:

That’s it!

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

