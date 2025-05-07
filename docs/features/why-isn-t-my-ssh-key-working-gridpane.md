# Why isn’t my SSH Key working? | GridPane

# Why isn’t my SSH Key working?

 

2 min read 

## Introduction

If this is the first time you’ve started to use SSH keys and connect to your servers, a common getting started issue is your newly created SSH key not working correctly.

This can be due to incorrect formatting, or the key your trying to push to your server has already been assigned to an existing system user.

 

## Incorrect Formatting

If your SSH key isn’t working, it’s usually because it’s not formatted correctly. The most common two things we see when are:

There should be a space between ssh-rsa and the key itself – see the correct formatting example below.

 

### Incorrect Formatting Example

This is an example of a key that is NOT formatted correctly:

```
ssh-rsa 
AAAAB3NzaC1yc2EAAAABJQAAAQEAxznqQ5ic/ctZi1AKS6ysTYo+v3fsADTLup
HqvvtgK0WfFtFYEvdAKjIz1abMXH5srFs6mqDJ56jxtxc9alBnINanKsnYmEzP
3cdcJTREA/BUoShSonXNL3pJs8dtJovldejw6QPB2S2Wnt4FfFOHidwilN15xb
K3PrPqdGyqrmvMkqXRRABfosAzhdLa9t26P9lhcKhEIWmeQipWgjVyNPkkEraa
7HkIPC04t8rjuMtBtHkZ0iv6SqU14d7pODcVR6/nPzm2SqTpDJ8LV8kx1v0ZHo
1k2XYHd6jCB38ns0kjVbPPmFhwUDoLaZa6esKAnJ+SnAc3JExL7Mw1ZtfEjQ==
 rsa-key-20200519
```

### Correct Formatting Example

This is an example of what an SSH key looks like when correctly formatted:

```
ssh-rsa AAAAB3NzaC1yc2EAAAABJQAAAQEAxznqQ5ic/ctZi1AKS6ysTYo+v3fsADTLupHqvvtgK0WfFtFYEvdAKjIz1abMXH5srFs6mqDJ56jxtxc9alBnINanKsnYmEzP3cdcJTREA/BUoShSonXNL3pJs8dtJovldejw6QPB2S2Wnt4FfFOHidwilN15xbK3PrPqdGyqrmvMkqXRRABfosAzhdLa9t26P9lhcKhEIWmeQipWgjVyNPkkEraa7HkIPC04t8rjuMtBtHkZ0iv6SqU14d7pODcVR6/nPzm2SqTpDJ8LV8kx1v0ZHo1k2XYHd6jCB38ns0kjVbPPmFhwUDoLaZa6esKAnJ+SnAc3JExL7Mw1ZtfEjQ== rsa-key-20200519
```

 

## Key is Already Assigned

Another reason it may not work is that you’ve already assigned that key to a system user. If that’s the case, you cannot push the same key to a server more than once.

In this situation, the easiest path forward is to create a new SSH key.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

