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

See the section _Running docker commands on your machine_ below for more
about how the local `docker` command works.

Once the install script is finished, confirm that the `dock` program 
is installed:

    $ dock --help

And, if you want to check the `docker` command too:

    $ docker --help 


Managing the VM
---------------

Boot the VM:

    $ dock start

SSH into it:

    $ dock ssh

You can shut it down:

    $ dock stop

Or destroy it:

    $ dock destroy


Customize the VM
----------------

You can boot the VM with a specific private IP. By default, it boots
at 192.168.0.222, but you can change it with the `--ip` flag:

    $ dock start --ip 192.168.0.10

You can boot a different Vagrant box too. By default, `dock` boots a 
Ubuntu 14.04 box (`ubuntu/trusty64`), but you can boot a different one
with the `--box` flag: 

    $ dock start --box hashicorp/boot2docker

You can also choose to sync a specific folder on your computer with the `dock` VM. By default `dock` replicates your home directory on the VM. For instance, on OS X, your home directory `~` is `/Users/<username>`, so `dock` makes a folder on the VM at `Users/<username` and syncs it with yours. But you can change this with the `--share <host_path>:<vm_path>` option. For instance:

    $ dock start --share ..:/usr/share

These options get saved in your Vagrantfile, so you don't have to specify 
them again until you want to change them. For instance, if you boot 
your VM with IP `192.168.0.10`, like this:

    $ dock start --ip 192.168.0.10

you then can later just do this:

    $ dock start

and it will boot with IP `192.168.0.10` again.


Running docker commands on the VM
---------------------------------

Once the VM is booted (with `dock start`), you can run any docker commands
you like on it. For instance, you can do

    $ dock docker ps

and you will see the output of `docker ps`, which `dock` executed on
the VM.


Running docker commands on your machine
---------------------------------------

If you ran the `./install` script with the `--with-local-docker` flag 
(see the _Installation_ section above), then you can execute many
regular docker commands directly on your machine, as if docker were
installed locally. For instance, you can type:

    $ docker ps

and see the output of `docker ps` directly.

Under the hood, this just forwards the `docker ps` command on to the VM; 
it gets executed on the VM, not on your local machine.
