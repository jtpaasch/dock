DOCK
====

Use docker on a Vagrant VM.

This program is a wrapper around a Vagrant VM with docker on it. It
handles the creating/booting/managing of the VM, and it proxies docker 
commands to the VM.


Requirements
------------

* OS 10.11 (Does it work on Linux? Maybe?)
* Bash 3.2+
* Virtualbox 5.0+
* Vagrant 1.7.4+


Installation
------------

Clone the repo, navigate into the directory where you downloaded it,
and then run the install script:

    $  ./install 

That should make the `dock` command available on your system.

If you want to install a proxy `docker` command on your system too,
run the install script with a `--with-local-docker` flag:

    $ ./install --with-local-docker

See the section *Running docker commands on your machine* below for more
about how the local `docker` command works.

Once the install script is finished, confirm that the `dock` program 
is installed:

    $ dock --help

And, if you want to check the `docker` command too:

    $ docker --help 


Managing the VM
---------------

Initialize the dock VM:

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

    $ dock up --box hashicorp/boot2docker

To mount your current working directory to a specific path 
on the VM (instead of the default `/usr/local/workdir`):

    $ dock up --synced-folder /var/app

These options get saved in your Vagrantfile, so you don't have to specify 
them again until you want to change them. For instance, if you boot 
your VM with IP 192.168.0.10, like this:

    $ dock up --ip 192.168.0.10

you then can later just do this:

    $ dock up

and it will boot with IP 192.168.0.10 again.


Running docker commands on the VM
---------------------------------

Once the VM is booted (with `dock up`), you can run any docker commands
you like on it. For instance, you can do

    $ dock docker ps

and you will see the output of `docker ps`, which `dock` executed on
the VM.


Running docker commands on your machine
---------------------------------------

If you ran the `./install` script with the `--with-local-docker` flag 
(see the *Installation* section above), then you can execute many
regular docker commands directly on your machine, as if docker was
installed locally. For instance, you can type:

    $ docker images

and see a list of any docker images. 

Under the hood, this just forwards your `docker` command on to the VM; 
it gets executed on the VM, not on your local machine.
