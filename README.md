# share-ssh
share-ssh script simply connects to a remote host, but also uses the multiplexing option if available.
In case that the multiplexing is not enabled on the client, the connection would be established without that option.
## share-ssh-profile
share-ssh-profile is an additional tool for easy adding a profile to gnome-terminal to use share-ssh as a command shell.
This tool is manipulating dconf data, and should be used with caution.
## Linux distribution
share-ssh-profile was written for ubuntu 20.04 distribution with gnome desktop
## Requirement
share-ssh script is using *host* command. make sure it is installed ```apt install bind9-host```
share-ssh-profile is using *dconf* command, which is a part of dconf-cli package
## Installation
Basic installation:
```
./configure
make install
```
The default installation location is ~/.local. to change it run 
```./configure --prefix=/path/to/install```
Replace /path/to/install with your prefered location
List more configuration options with 
```./configure --help```
After running ```./configure```, install the tools with the command
```make install```
## Using the tools
### Prompt to a host name
```share-ssh```
### Connect to host that listed on ~/.ssh/config with the name my:
```share-ssh my```
### Connect to host with full domain name and parameters
```share-ssh my-workstation.organization.com -X```
In case you have configured with --default-domain, you can ssh to hosts in that domain without their full domain name, even if it is not in your search path.
### Adding profile to gnome-terminal
```share-ssh-profile [hostname [parameters ...]]```
The first parameter is the host name to connect to, if it omitted the profile will show a prompt for the host name to connect to.
## Configure openssh client
To configure multiplexing on your ssh client, you have to set a control path and enable control master. Edit your ~/.ssh/config file and add the lines:
```
Host *
    ControlMaster auto
    ControlPath ~/.ssh/master-%r@%h:%p.socket
```

You can set specific entries to some hosts, like:
```
Host my
	HostName my-workstation.organization.com
	ControlMaster auto
	ControlPath ~/.ssh/ssh-%r@%h:%p
```
