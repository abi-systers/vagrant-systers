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

# Environments included

This repo includes two different versions of mailman for development: 1) mailman
2 with systers patches 2) mailman 3 development environment. They are split
between the following directories which you need to cd into to run the commands
below:

* mm2 == Mailman 2 with systers patches
* mm2-32bit == Mailman 2 with systers patches on i686
* mm3 == Mailman 3 development environment

# Using Vagrant

The Vagrantfile is setup to automatically download a VM image that already has
the Systers mailman configured and already deployed. Make sure you cd into one
of the environments before running the commands below.

## Starting a VM

    vagrant up

**NOTE: If you get an error that a port is currently being used, open up the
Vagrantfile and change the port to something else (the second port number listed
in the file).**

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

# Systers Mailman 2 Environment

Please make sure you are in the `mm2` directory when running the vagrant
commands above for this environment.

## Accessing the Mailman web interface

You can access the mailman web interface by going to
[http://localhost:8080/mailman/listinfo](http://localhost:8080/mailman/listinfo)
in your browser.

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

# Mailman 3 Environment

Please make sure you are in the `mm3` directory when running the vagrant
commands above for this environment.

This environment has been setup following [Meflin's CentOS install
documentation](http://www.meflin.net/mm3.txt) and the [5 minute dev
guide](http://wiki.list.org/display/DEV/A+5+minute+guide+to+get+the+Mailman+web+UI+running).
All of the code has been checked out as the root user in its home directory in
`/root`.

## Starting mailman

Make sure you are the root user.

    cd mailman
    bin/mailman start

## Starting the web gui

Make sure you are the root user.

**NOTE: Please notice the runserver command is different than what's included in
the documentation above.**

    cd postorius_standalone
    python manage.py runserver 0.0.0.0:8000

## Connect to the GUI

Open a browser and connect to [http://localhost:8000/](http://localhost:8000/).
The admin user is `root` and the password is `vagrant`.

vi: set tw=80 ft=markdown :
