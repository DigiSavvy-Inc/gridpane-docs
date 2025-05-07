# Using Domain Names with International Characters | GridPane

# Using Domain Names with International Characters

 

1 min readIf you’re trying to add a website to GridPane and the domain name has international characters (e.g. é and ä), you will first need to convert it into “Punycode” before you can provision them as a website on your server.

Punycode is a representation of Unicode with the limited ASCII character subset used for Internet hostnames. – Wikipedia

As an example, if we were to try and provision gridpäné.com, the UI would return an “invalid format” error, as it needs to first be converted into punycode.

To run the conversion, there’s a handy website called Punycoder that can do this for:
https://www.punycoder.com/

Here’s how gridpäné.com would look:

So gridpäné.com won’t provision on your server, but “xn--gridpn-fua5b.com” will, and this is the correct format.

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

