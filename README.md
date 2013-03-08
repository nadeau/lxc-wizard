Perl script for Linux Containers creation
=========================================

Read the top of the script for full documentation and patch it for your personal use


Build cache OS
--------------

This uses debootstrap to install a base debian under /var/cache/lxc

    # lxc-wizard --BUILD
    
    ** Container Creation Wizard **
    Creating cache directory... OK
    Creating download directory... OK
    Downloading Debian minimal...
    I: Retrieving Release
    I: Retrieving Packages
    I: Validating Packages
    I: Resolving dependencies of required packages...
    I: Resolving dependencies of base packages...
    I: Found additional required dependencies: insserv libbz2-1.0 libdb4.8 libslang2 
    I: Found additional base dependencies: adduser debian-archive-keyring gnupg gpgv libbsd0 libdb4.7 libedit2 l 
    ibgdbm3 libgpm2 libgssapi-krb5-2 libk5crypto3 libkeyutils1 libkrb5-3 libkrb5support0 libncursesw5 libreadlin 
    e6 libssl0.9.8 libusb-0.1-4 libwrap0 openssh-blacklist openssh-client perl perl-modules procps readline-comm 
    on vim-common vim-runtime 
    I: Checking component main on http://mirror.peer1.net/debian...
    I: Retrieving libacl1
    I: Validating libacl1
    I: Retrieving adduser
    I: Validating adduser
    ...
    Setting up sgml-base (1.26+nmu1) ...
    Setting up xml-core (0.13) ...
    Processing triggers for python-support ...
    OK


Update cached OS
----------------

Upgrades your debian fs under /var/cache/lxc

    # lxc-wizard --REFRESH

    ** Container Creation Wizard **
    Get:1 http://mirror.peer1.net squeeze Release.gpg [1672 B]
    Get:2 http://mirror.peer1.net squeeze/updates Release.gpg [836 B]
    Get:3 http://mirror.peer1.net wheezy Release.gpg [836 B]
    Get:4 http://mirror.peer1.net wheezy/updates Release.gpg [836 B]
    ...
    Fetched 9501 kB in 3s (2891 kB/s)
    Reading package lists... Done
    Reading package lists... Done
    Building dependency tree       
    Reading state information... Done
    0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
    OK


Configure new container
-----------------------

    # lxc-wizard --help

    ** Container Creation Wizard **
    Usage: lxc-wizard [options]
    
        --fqdn DQDN         full qualified domain name of the target container
        --hostname HOST     hostname (if it can't be extracted from the fqdn)
        --domain DOMAIN     domain name (if it can't be extracted from the fqdn)
        --ipaddr IPADDR     ip address (if it can't be found by gethost call)
        --gwaddr IPADDR     gateway address
    ...


    # lxc-wizard --fqdn coral.gene

    ** Container Creation Wizard **
    Please enter the following information
    default values in [], hit enter to accept
    
    Container FQDN [coral.gene] : 
    IP Address [10.5.2.2] : 
    GW Address [10.5.0.1] : 
    Container LXC Name [Coral] : 
    Create Logical Volume [Y] : 
    Logical Volume Group [bigfoot] : 
    Logical Volume Name [Coral] : 
    Logical Volume Size [32G] : 16G
    Mount Point [/var/lib/lxc/Coral] : 
    Container Memory Limit [8G] : 4G
    Container Memory+Swap Limit [4G] : 
    Container CPU Shares [1024] : 
    Container IO Weight [1000] : 500
    Install container OS [Y] : 
    Set to autostart on boot [Y] : N
    Start container when finished [Y] : 
    
    Please verify all information:
    
    Container Name:        Coral
    Container FQDN:        coral.gene
    Container IP:          10.5.2.2
    Container GW:          10.5.0.1
    
    Create Logical Volume: Y
    Volume Group:          bigfoot
    Volume Name:           Coral
    Volume Size:           16G
    Mount Point:           /var/lib/lxc/Coral
    
    Memory Limit:          4G
    Memory+Swap Limit:     4G
    CPU Shares:            1024
    IO Weight:             500
    
    Set to start on boot:  N
    Start after setup:     Y
    Install OS:            Y
    
    Is everything right [Y] : 
    
    Creating Logical Volume...   Logical volume "Coral" created
    OK
    Creating Filesystem... mke2fs 1.41.12 (17-May-2010)
    Filesystem label=Coral
    OS type: Linux
    Block size=4096 (log=2)
    Fragment size=4096 (log=2)
    Stride=0 blocks, Stripe width=0 blocks
    1048576 inodes, 4194304 blocks
    0 blocks (0.00%) reserved for the super user
    First data block=0
    Maximum filesystem blocks=4294967296
    128 block groups
    32768 blocks per group, 32768 fragments per group
    8192 inodes per group
    Superblock backups stored on blocks: 
            32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632, 2654208, 
            4096000
    
    Writing inode tables: done                            
    Creating journal (32768 blocks): done
    Writing superblocks and filesystem accounting information: done
    
    This filesystem will be automatically checked every 26 mounts or
    180 days, whichever comes first.  Use tune2fs -c or -i to override.
    OK
    Tuning Filesystem... tune2fs 1.41.12 (17-May-2010)
    Setting maximal mount count to -1
    Setting interval between checks to 0 seconds
    OK
    Creating Mount Point... OK
    Mounting Filesystem... OK
    Updating /etc/fstab... OK
    Copying cached container template... OK
    Starting container... Can't exec "lxc-start": No such file or directory at lxc-wizard line 316, <STDIN> line 17.
    error!
    Abort [A] or Continue [C]? C
    Shit happened.

Comprehensive error management is implemented for your convenience.
