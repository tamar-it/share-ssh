# share-ssh
share-ssh script simply connect to remote host, but also using the multiplexing option if available.
In case that the multiplexig is not enable on the client, the connection would established without that option.
## share-ssh-profile
share-ssh-profile is additional tool to easy add a profile to gnome-terminal to use share-ssh as a command shell.
This tool is manipulating dconf data, and should be used with caution. 
## Linux distribution
share-ssh-profile was written to ubuntu 20.04 destiribution with gnome desktop
## Requirement
share-ssh script is using *host* command. make sure it is installed ```apt install bind9-host```
share-ssh-profile is using *dconf* command, which is a part of dconf-cli package
## installation
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
In case you configured with --default-domain, you can ssh to hosts in that domain without thier full domain name, even if it is not in your search path.
### Adding profile to gnome-terminal
```share-ssh-profile [hostname [parameters ...]]```
The first parameter is the host name to connect to, if it ommited the profile will show prompt for the host name to connect to.
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
