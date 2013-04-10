# Vagrant file for a Systers Mailman development environment.

A [Vagrant](http://vagrantup.com/) file used for deploying a CentOS 6 based
environment with the latest production version of the
[Systers](http://anitaborg.org/initiatives/systers/) [patched
Mailman](https://launchpad.net/systers). This VM is setup very close to how the
production instance.

# Requirements

* VirtualBox >=4.1.x
* vagrant >=1.0.3

# Setup

1. Install VirtualBox by going to their [download
page](https://www.virtualbox.org/wiki/Downloads).

2. Install Vagrant

    `gem install vagrant`

If you need more help installing Vagrant, please take a look at [their
installation documentation](http://docs.vagrantup.com/v2/installation/).

# Using Vagrant

The Vagrantfile is setup to automatically download a VM image that already has
the Systers mailman configured and already deployed.

## Starting a VM

    vagrant up

## Accessing the VM

    vagrant ssh

The initial login will be as the `vagrant` user. If you need root privileges
just type `sudo su -`. 

Any files that reside in the directory which contains the Vagrantfile will show
up inside of the VM as `/vagrant` so that you are free to edit files from your
workstation outside the VM if you want.

## Shutting down the VM

    vagrant halt

## Deleting the VM and starting fresh

**NOTE: This will delete any files on the VM itself. Please be careful!**

    vagrant destroy
    vagrant up

# Systers Mailman

## Accessing the Mailman web interface

You can access the mailman web interface by going to
http://localhost:8080/mailman/listinfo in your browser.

The site admin password is `systers` and the password for the systers-admin list
is `systers` as well.

## Testing email functionality

The system will send email however it has no way of accepting email from outside
of the VM. So the only way to test email efficiently is by sending mail to
local users on the VM itself.

[Mutt](http://www.mutt.org/) has been installed so that you can send and read
email that has been sent locally on the VM. You will not be able to use a
regular mail client to send mail since the VM is running local so mutt is the
best option. If you are not familiar with Mutt, check out their [getting started
documentation](http://www.mutt.org/doc/manual/manual-2.html) to learn more about
the basic commands.

The following email addresses should work locally on the VM:

* root@systers-dev.systers.org
* vagrant@systers-dev.systers.org

If you need more addresses just create additional local users. You will have to
be logged in as the user to view their mail however (use sudo and su).

## Development procedures

**TODO: More details to come but some basics below.**

The files are installed in various directories on the system, but for a
reference you can find them here:

    /etc/mailman-systers        # mailman config files
    /usr/lib/mailman-systers    # mailman python files, binaries, etc
    /var/lib/mailman-systers    # mailman data, lists archives, etc
    /var/log/mailman-systers    # mailman logs

To access mailman more directly via the command line, just type `sudo su -
mailman` which will put you in the `/usr/lib/mailman-systers` folder.

To access postgres, run `sudo su - postgres` and then `psql`.

vi: set tw=80 ft=markdown :
