# Getting to know the command line: Linux CLI basics | GridPane

# Getting to know the command line: Linux CLI basics

 

16 min read 

### Table of Contents

 

## Introduction

Connecting to your server for the very first time can be a daunting task, especially for non-developers. At some point in your GridPane journey, you’re likely going to need to SSH in and run a few commands.

Fortunately, you really don’t need to know a whole lot to take advantage of what GridPane has to offer, and it is much simpler than it appears at first glance. If you’re concerned that you’ll accidentally break things, you should know that this isn’t actually that easy to do. Just to be sure though, you may wish to spin up a test server for a couple of days so you’re free to do whatever you wish with zero real-world consequences for you or your clients.

GridPane allows you to do some very cool things (especially with GP-CLI) very quickly, simply by typing a few commands inside your server. The goal of this article is to give you the info you need to get comfortable connecting to your servers and running basic commands. If you take just a little time to get comfortable and build your skills, the entire GridPane knowledge base will become accessible to you whenever you need anything contained herein.

Using the command line can make your new website setup and management much more efficient and it is worth taking the time to learn the fundamentals.

 

## Part 1. A Quick Introduction to SSH

SSH stands for “Secure Shell”. It’s a method of securely connecting from one computer to another. In our case, it allows us to connect directly to our servers so that we can access and manage them.

It’s the most common way for safely managing remote servers, and on GridPane, it is the only method we allow for connecting to your servers.

SSH uses numerous encryption technologies (symmetric encryption, asymmetric encryption, and hashes) to verify and secure your connection to your server and your server to you.

 

### SSH and WordPress

If you’ve been around hosting for any length of time you’ve likely connected to your servers via FTP or SFTP and you’ve seen all of your website’s files and folders.

SSH won’t allow you to directly upload or download files from your computer, but it will allow you to view and edit them, zip them ready for download, unzip uploaded zip files, take database backups, and more.

Connecting and managing your sites via SSH is fast, secure, and efficient, and this is why sysadmins use the command line to manage WordPress instead of logging into each site’s dashboard. It’s highly unlikely that you’ll ever go back the traditional way once you get started.

 

### Connecting to your server by SSH

We have numerous guides on how to create a public and private SSH key, and add your public key to your GridPane servers. Please see the following guides to get yourself set up and ready to go.

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

## Part 2. Navigation – Commands you’ll use a lot

There are some commands that are key to navigating around and viewing the contents of your server. You’ll likely use them almost every time you SSH in, and they also happen to be great first commands to learn as you can’t break anything with them.

Quick tip: Always make sure to type a space between a command and any parameters.

 

### ls – The list command

The ls command allows you to view the contents of a directory by displaying all the files and folders in a list. Typically, you’ll use the ls -l command (detailed below), as it displays the information in a more visually friendly way, but you will use this command a lot.

Variations

There are many more variations than those listed below, however, these will be the most useful to get you started.

ls -l This will display the directory contents with each file/folder on its own line and include its permissions

ls -a This will display all files including any hidden files

ls -lh This will list each file/directory on its own separate line and display the file size in human-readable form

ls -lah This will do the same as above and include hidden files

ls -s This will display files in columns

ls -s -h This will display files in columns with the file size in human-readable form

 

### cd – Change Directory

The cd command will allow you to navigate around your server, changing from one directory to another. Typically you’ll combine it with the list commands above in order to locate the directories you’re looking for and make your way to them.

To use the cd command, you’ll need to follow it with a space and then your desired destination. For example, you can navigate to the folder where all of your websites are stored with:

```
cd /var/www/
```

You could then run ls -l to view all of your websites.

Variations

The following do not require a directory to work. They’re handy shortcuts that will save you from typing out (or copying/pasting) directories when it’s simply not necessary.

cd ~ This will take you to the root directory.

cd .. This will take you to the directory immediately above your current location.

cd - This will take you to the previous directory.

 

### Arrow keys, Home & End

Technically these aren’t commands but they will come in very handy.

Using the up arrow key will allow you to go back through the commands you’ve previously run, saving you the time it takes to write them out again. Simply press the up key to get started, and you can navigate back and forth using both the up arrow key and down arrow keys.

Home, End, and the side arrow keys work exactly as you’d expect.

 

## Part 3. Active Server Management Commands

This is part will detail the commands that will allow you to actively make changes to your server. This includes how to move, copy, delete, zip, unzip and more.

 

### Create a directory

You can make (create) a directory with the mkdir command. To do this, you can either navigate to where you wish to create your new directory, or you create it using the full path.

For example, if you wanted to create an extra folder in your htdocs folder you could:

```
cd /var/www/yourwebsite.com/htdocs
```

And then:

```
mkdir mynewdirectory
```

Or you could create it with:

```
mkdir /var/www/yourwebsite.com/htdocs/mynewdirectory
```

 

### Creating new files

You can create a new file with the touch command. However, normally you’ll use nano filename.extension to create a file and open it with the nano editor at the same time. More information on this is in part 4.

An example using the touch command is:

```
touch newphpfile.php
```

 

### Copy

You can create a copy of a file or folder with the cp command. This can come in very handy if you wish to make a copy of a file before editing, and it’s also useful for making certain Nginx changes persistent (you may see this in various other KB articles).

To use this command, you first type cp followed by the file you wish to make a copy of, followed by the desired location and filename of your copy. For example:

```
cp main-context.conf /_custom/main-context.conf
```

Think of the command like so:

```
cp SOURCE DESTINATION
```

Variables

Below are some useful variations of the cp command.

cp -f If there is already another file with the same name in the destination you’re copying to, this will override that file with the one you are copying.

cp -i This will give you a warning message before copying if a file with the same name already exists.

cp -n This will stop the copy from proceeding if there’s an existing file with the same name in the destination.

 

### Move

The mv command will allow you to move files and directories from one place to another.

```
mv SOURCE DESTINATION
```

Variations

mv file.ext /dir/ This moves to the directory you specify.

mv file.ext/ .. This will move the file up one directory.

mv file.ext /dir/newname.text This variation will both move and also rename the file.

 

### Viewing the contents of existing Files

The following commands will allow you to view the contents of a file.

cat This will display the entire contents of a file. Example usage:

```
cat wp-config.php
```

Or you can use the whole destination:

```
cat /var/www/example.com/wp-config.php
```

head This will display the first 10 lines of a file. Example usage:

```
head wp-config.php
```

tail This will display the last 10 lines of a file. Example usage:

```
tail /var/www/example.com/wp-config.php
```

tail -f View a file in real-time. This is particularly useful for viewing logs while you’re running commands or using the GridPane control panel to toggle things on and off. Here’s an example worth noting down:

```
tail -f /var/log/gridpane.log
```

 

### Remove (delete) stuff

You can remove (DELETE) files and directories from your server with the rm command. This is where you need to start being careful as removing files and directories has real consequences that can/will affect your sites and servers. That said, it is still useful to know and will come in handy at some point down the line.

Here’s a simple example of removing a text file:

```
rm myoldfile.txt
```

You can also delete multiple files at once like this:

```
rm myoldfile1.text myoldfile2.text myoldfile3.txt
```

rm -r directoryname – This is a powerful command that can save a lot of time vs trying to do the same thing over SFTP. It will delete the directory and ALL of its contents. This means all sub-directories and files inside it.

So, for example, you could remove an entire website’s htdocs folder with:

```
rm -r /var/www/example.com/htdocs
```

Obviously, we don’t recommend you test that, but removing an entire htdocs folder can be handy for manual website migrations.

rmdir This command can be used to remove (delete) an empty directory. Example usage:

```
rmdir directoryname
```

 

### View File sizes

The du (disk usage) command is great for checking how much disk space usage each of your websites and other files/directories are taking up on your servers. Used on its own usually isn’t going to be all that useful, but the variations below are well worth knowing.

Variations

du -h Displays results in human-readable format (bytes, KB, MB, GB etc).

du -sh Displays the grand total disk space of a directory in a human-readable format.

Here is a useful, more advanced command that you may wish to copy down. If you first navigate to the directory where all of your websites are stored with:

```
cd /var/www
```

This command will then list them by order of size (largest at the bottom), and display their size in human-readable format:

```
du -h --max-depth=1 | sort -h
```

 

### View System Disk Space

With Monit installed on all servers, you won’t have much need for this command. You can view your disk usage any time by clicking on the pie chart icon next to each of your servers. However, it would be odd to leave it out, so you can check your system disk space usage with the df command.

Variations

df -h Displays results in a human-readable format.

df -T This will display system file types in an additional column.

 

## Part 4. Creating and editing files

We touched on the touch command briefly in part 3 for creating a file, but the same can be accomplished with nano and this has the added benefit of opening your new file so you can begin adding your code to it immediately. For example:

```
nano newphpfile.php
```

You can create any type of file with nano by simply specifying the correct extension at the end of the file name. Examples: –

```
nano something-main-contenxt.conf
```

```
nano newtextfile.txt
```

```
nano style.css
```

Once you added your content to the file, you can save it with CTRL+O and then confirm with Enter. Or, you can save and exit at the same time with CTRL+X and then hit Y (for yes), and then Enter.

To exit nano, you need to CTRL+X. You will be prompted to save your changes or disregard them if you haven’t already saved them.

While there are other options available, we recommend using nano when given multiple options.

 

## Part 5. Working with Compressed Files

You may need to zip and unzip files when working on the command, or work with tar files.

Tar is short for “Tape Archive”, and is sometimes referred to as tarball. This type of file is in the “Consolidated Unix Archive format” and is used to archive multiple files into one single file. Regular tar files are not compressed. Compressed tar files are in the tar.gz format.

 

### Zip

The zip command is exactly what you think it is. It will zip up a directory. For example:

```
zip /var/www/example.com/htdocs
```

Variations

zip -m filename.zip foldername This compresses a folder and then deletes the original, leaving just the zipped version.

zip -d filename.zip foldername deletes a file from the existing zip archive you specify.

 

### Unzip

unzip is also exactly what it sounds like. You can use this command to unzip and zipped file as follows:

```
unzip filename.zip
```

If the zip file is passworded you will be prompted for the password after running the above.

Variations

unzip filename.zip -x excludeme.ext This will exclude a specific file from being extracted. To exclude a directory it looks like this:

```
unzip filename.zip -x "*.foldername/*"
```

unzip filename1.zip filename2.zip filename3.zip This will all you can unzip multiple files at the same time.

 

### List the contents of a Zip File

You can view the contents of a zipped file with unzip -l. For example:

```
unzip -l filename.zip
```

 

### Creating Tar Files

Tar has a few extensions that allow you to specify exactly how you wish to create your tar file: –

p This preserves the details of the file owner and file permissions in the archive.

c This is used to create a tar file.

v This will verbosely show the tar files progress while it’s being created.

z This enables gzip compression.

f This -f option means that next is the name of the target tar file.

To create a .tar file, you can use tar -cf. For example:

```
tar -cf tarfilename.tar /target/directory
```

To show what’s happening you can add in the -v. For example:

```
tar -cvf tarfilename.tar /target/directory
```

To compress the file and view the verbose output, add the -v and -z. Example:

```
tar -cvzf tarfilename.tar /target/directory
```

 

### Extracting Tar Files

Extracting tar files works the same as the way you create them, except instead of creating with -c we extract with -x. For example:

```
tar -xf tarfilename.tar
```

View the verbose output with:

```
tar -xvf tarfilename.tar
```

You can learn more about working with .tar files here: https://man7.org/linux/man-pages/man1/tar.1.html

 

## Part 6. Searching your system

If you need to find specific files or data in your server, there are a couple of powerful commands that you can use to find what you need.

 

### find – Find files and directories

Find files with the find command.

The syntax is as follows:

```
find starting/path criterion "search term"
```

Starting/pathHere you can specify a specific directory, for example, you could search only your website files with the starting path: /var/www. Or, you can use the following as your starting path: –

/ A single slash will search the whole system.

. A dot will search the directory you’re currently in.

CriterionYou can narrow down your search with the following criteria: –

-name Search by file name.

-user Search files belonging to a specific system user.

-size Search files of a specific size.

-type d Search only for directories.

-type f Search only for files.

-maxdepth X Search the current directory as well as all sub-directories X levels deep.

Below are some examples to illustrate.

Search for all wp-config.php files inside of /var/www: –

```
find /var/www -name wp-config.php
```

Search for all directories named “htdocs” inside of /var/www: –

```
find /var/www type d -name htdocs
```

Search for the main-context.conf inside /etc: –

```
find /etc -name main-context.conf
```

 

### grep – Search files by content

Grep stands for “global regular expression print”. It allows you to search for files based on their content, and search inside files for specific strings of data.

It’s an incredibly powerful tool and it can be combined with the find command. Here we’ll just touch on the basics.

Here’s a simple example of using the grep command to search a file for a specific phrase:

```
grep searchword/term filename
```

Let’s search a websites wp-config.php file for the word “prefix”: –

```
grep prefix /var/www/example.com/wp-config.php
```

Variations

grep -i searchword/term filename This searches for all variations of a search word/term ignoring the case (grep is case-sensitive).

grep -c searchword/term filename This will count the number of instances of a search word/term in the file.

grep -n searchword/term filename This will display the line number/s along with the output.

grep -l searchword/term */path This will list all the files that contain the search word/term.

There is a whole lot more to the grep command that we’ll look at covering another time.

 

## Part 7. Monitoring your system

Linux comes with the built-in monitoring tool top. By default, we also install htop on your servers during provisioning. Both of these are extremely useful tools that you can open simply by typing their names. Go ahead and give it a go (and then exit them with CTRL+C).

We have separate knowledge base articles for using each of these tools. You can check them out here:

How to use the top command to monitor system processes and resource usage

How to use the htop command to monitor system processes and resource usage

 

## Part 8. Other useful commands

Here are a few more commands that will come in handy on your Linux journey.
### wget – Download from a website

You can download a file from a source outside of your server with the `wget` command. The syntax for this is as follows:

```
wget OPTIONS URL
```

The options are optional. For example, you could download a file to your current directory like this:

```
wget https://example.com/optimuscacheprime.tar.gz
```

You can download a file to a different directory like this:

```
wget /save/file/here https://example.com/optimuscacheprime.tar.gz
```

Learn more here: [https://linux.die.net/man/1/wget](https://linux.die.net/man/1/wget)
### pwd – Print name of current/working directory

`pwd` will show you the filepath of exactly where you are on your server.
### Clear your terminal window

If you ever wish to clear your terminal so that it’s nice and clean and not full code, you can do this in a couple of ways.

`clear` Type clear and hit enter.

Hit CTRL+L.

Both of these will clear all of the text from your screen, leaving you with a nice and tidy terminal to continue working in.								

## Part 9. The Linux Manual

Linux comes with a user manual built-in. If you wish to learn more about any of the commands in this article you can look them up inside the Linux manual and see their variations plus a description of what they all do.

To use the Linux manual, you can use the man command. For example:

```
man whatis
```

Linux also has another command called whatis. This will display a one-line manual page description for the command you’re looking up. For example:

```
whatis tar
```

You can learn more by looking it up directly in the Linux manual 🙂

 

## Part 10. Exit

And, finally, you can exit (disconnect from) your servers with:

```
exit
```

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

