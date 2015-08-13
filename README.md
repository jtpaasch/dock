DOCK
====

Manage docker images and containers on a Vagrant VM.

This script is a wrapper around a Vagrant VM with docker on it. It handles the creating/booting/managing of the VM, and it proxies docker commands to the VM.


Requirements
------------

* OS 10.11 (Linux maybe?)
* Bash 3.2+
* Virtualbox 5.0+
* Vagrant 1.7.4+


Installation
------------

Clone the repo, and then run `./install`. That should make 
the `dock` command available on your system. 

Get quick help:

    $ dock --help

When the `install` script finishes, you may notice a note about 
forwarding docker commands to the VM. See the section *Forwarding
docker commands* below for more on that.


Managing the VM
---------------

Make a folder to do your work in:

    $ mkdir myproject && cd myproject

Initialize the folder:

    $ dock init

Now you can boot the VM:

    $ dock up

SSH into it:

    $ dock ssh

You can shut it down:

    $ dock down

Or destroy it:

    $ dock destroy


Customize the VM
----------------

You can customize the VM's boot settings. To make it run on a 
specific private IP (instead of the default 192.168.0.222):

    $ dock up --ip 192.168.0.10

To use a different Vagrant box (instead of the default 
Ubuntu 14.04 box `ubuntu/trusty64`):

    $ dock up --box ubuntu/vivid64

To mount your current working directory to a specific path 
on the VM (instead of the default `/usr/local/workdir`):

    $ dock up --synced-folder /var/app

These options persist after you specify them once, because they get
saved in your Vagrantfile, so you don't have to specify them again. 
For instance, if you boot your VM with IP 192.168.0.10, like this

    $ dock up --ip 192.168.0.10

you then can later just do this

    $ dock up

and it will boot with IP 192.168.0.10 again.


Running docker commands
-----------------------

Once the VM is up (with `dock up`), you can run any docker commands
you like, and they will be passed to the VM. For instance, you can
do

    $ dock docker ps

and you will see the output of `docker ps`, which was executed on
the VM.


Forwarding docker commands
--------------------------

When the `install` script finishes, it will mention that if you want to 
forward docker commands to the VM, you should add something like the
following to your bash profile:

    function docker { dock docker "$@"; }

If you add that line to your bash profile (`~/.bash_profile` on OS X, 
`~/.profile` on Ubuntu, etc.), you will be able to execute docker commands
directly on your machine, as if docker was installed locally.
