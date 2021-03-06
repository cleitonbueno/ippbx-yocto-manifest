Build IP-PBX with Asterisk to Toradex Colibri iMX6 with Build System Yocto Project
=============================================
This repository provides Repo manifests to setup the Yocto build system.

***
**Note:**
If you already have a Yocto Project setup and want only the B2Open layer, 
use the meta-b2open repository found here: 
git://github.com/cleitonbueno/meta-b2open.git.
***

The Yocto Project allows the creation of custom linux distributions for embedded
systems.  It is a collection of git repositories known as *layers* each of which 
provides *recipes* to build software packages as well as configuration information.

Repo is a tool that enables the management of many git repositories given a 
single *manifest* file.  Tell repo to fetch a manifest from this repository and
it will fetch the git repositories specified in the manifest and, by doing so,
setup a Yocto Project build environment for you!

Getting Started
---------------
**1.  Install Repo.**

Download the Repo script:

    $ mkdir ~/bin
    $ PATH=~/bin:$PATH

    $ curl http://commondatastorage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
    $ chmod a+x ~/bin/repo

Make it executable:

    $ chmod a+x repo


If it is correctly installed, you should see a Usage message when invoked
with the help flag.

    $ repo --help

**2.  Initialize a Repo client.**

Create an empty directory to hold your working files:

    $ mkdir ippbx-yocto
    $ cd ippbx-yocto

Tell Repo where to find the manifest:

    $ repo init -u git://github.com/cleitonbueno/ippbx-yocto-manifest.git -b krogoth

A successful initialization will end with a message stating that Repo is
initialized in your working directory. Your directory should now
contain a .repo directory where repo control files such as the manifest are
stored but you should not need to touch this directory.

**Note:**
You can use the **-b** switch to specify the branch of the repository
to use.  This project use branch krogoth.


**3.  Fetch all the repositories:**

    $ repo sync

Now go turn on the coffee machine as this may take 30 minutes depending on
your connection.


**4.  Initialize the Yocto Project Build Environment.**

    $ source setup-environment


**5.  Build an image:**

This process downloads several gigabytes of source code and then proceeds to
do an awful lot of compilation so make sure you have plenty of space (50GB minimum), 
and expect various hours or so of build time depending on your network connection.
Don't worry --- it is just the first build that takes a while.

    $ bitbake ippbx-image

Only download to later build:

    $ bitbake -c fetchall ippbx-image

The end result of the build will be in:
    
    build/tmp/deploy/images/colibri-imx6/


**6. Flash your image:**

Note that your uSD will have to be at least 2GB large. Pop in your micro SD card to your card writer, and find out the location of
the block device by running `dmesg`. Now you can run the script as following:

    $ sudo gunzip -c ippbx-image-colibri-imx6.sdcard.gz | sudo dd of=/dev/sdX bs=1M

If no errors occur, done!



License
-------------------

**MIT License**


Suggestions/Problems
-------------------
**E-mail:** cleiton.bueno at b2open.com

**Site:**   www.b2open.com

Good fun! \@/

