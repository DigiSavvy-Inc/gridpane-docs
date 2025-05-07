# I reset my Root Password at my Provider and now I am locked out… how do I get back in? | GridPane

# I reset my Root Password at my Provider and now I am locked out… how do I get back in?

 

1 min readGridPane only allows root access by SSH key. When we provision a server we lock down root access by password authentication.

When you reset your root password at your infrastructure provider it is a two step procedure.

Step 1. Reset password and receive new temporary password
Step 2. Login in to server and complete password reset.

The password your provider will issue you is only temporary, *nix requires you to login and complete the password reset by first entering the temporary password, and then choosing a new password and entering it twice, the second time to confirm.

Until this process is completed no remote commands can be issued on your server, which means that GridPane is essentially paused on the server.

If you have been following our recommended best practices, and using an SSH key for your root user, this is no problem.  Just log in by SSH and complete the process.

If you do not have an SSH key on your server, please contact support and provide the support team with your temporary password. A member of support will SSH in to your server by proxy via the GridPane app server and complete the process.

Once the process has been completed, GridPane will be reconnected and you can add your SSH key to the server as root and be able to log in as usual.

Resetting the root password at provider will not enable password login by root, we will always endeavour to make sure root user login is locked down to SSH key pair access only.

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

