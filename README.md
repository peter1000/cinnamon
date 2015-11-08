## Ports for constructing the 'cinnamon' and 'cinnamon-extra' collections

Contributions are welcome. If you don't know what it all about, please take the time to read the documentation at
http://www.nutyx.org/en/build-package.html
(version française)
http://www.nutyx.org/fr/build-package.html

It will explain you what's a collection, a git, a port, the tools around 'cards' etc

### How to test this git:

#### 1. Clone it in your home directory

    $ cd
    $ git clone git://github.com/NuTyX/cinnamon.git
    $ git clone git://github.com/NuTyX/gnome.git
    $ git clone git://github.com/NuTyX/current.git

#### 2. Become root until the end, define and create the directory used by the scripts:

 The script is checking the files /etc/install-houaphan.conf and /etc/install-houaphan.conf.d/cards.conf if they exist, if yes it will use them, so:

    $ su -
    # echo "LFS=/mnt/lfs
    DEPOT=/8.0
	VERSION=current" > /etc/install-houaphan.conf
    # mkdir -p /etc/install-houaphan.conf.d
    # cat > /etc/install-houaphan.conf.d/cards.conf << "EOF"
    dir  /8.0/cinnamon
    dir  /8.0/gnome-extra|http://downloads.nutyx.org
	dir  /8.0/gnome|http://downloads.nutyx.org
	dir  /8.0/gui|http://downloads.nutyx.org
	dir  /8.0/cli|http://downloads.nutyx.org
    dir  /8.0/base|http://downloads.nutyx.org
    dir  /8.0/base-extra|http://downloads.nutyx.org
    base /8.0/base
    base /8.0/base-extra
    logdir /var/log/pkgbuild
    EOF

#### 3. Install a base NuTyX system (assume below the user is 'lfs' so adapt to yours)

    # bash /home/lfs/current/scripts/install-houaphan

#### 4. In your chroot Make the directory where the git copy will comes

    # mkdir -v /mnt/lfs/root/{current,gnome,cinnamon}

#### 5. Mount your git project (assume below the user is 'lfs' so adapt to yours)

    # mount -o bind /home/lfs/cinnamon /mnt/lfs/root/cinnamon
    # mount -o bind /home/lfs/gnome /mnt/lfs/root/gnome
    # mount -o bind /home/lfs/current /mnt/lfs/root/current

#### 6. Enter now in your chroot (assume below the user is 'lfs' so adapt to yours)

    # bash /home/lfs/current/scripts/install-houaphan -ec

#### 7. Prepare the first execution of the build script

    # get cards.devel wget vim rsync git tar
 
#### 8. If everything is OK, synchronize the  current 'base', 'cli' , 'gui' and 'gnome' collections binaries

    # cd /root/current
    # bash scripts/base -s
    # bash scripts/cli -s
    # bash scripts/gui -s
    # cd /root/gnome
    # bash scripts/gnome -s
    # bash scripts/gnome-extra -s
    
#### 9. If everything is OK, synchronize the 'cinnamon' collection binaries 

    # cd /root/cinnamon
    # bash scripts/cinnamon -s

#### 10. If everything is OK, check with cards level what's new

    # cards level

 It should shows all the packages available.

#### 11. If you want to build the 'cinnamon' collection from the sources

    # bash scripts/cinnamon -a

#### 12. If you want to build the 'cinnamon-extra' collection from the sources, add the proper line in top of the cards.conf file like this:

    dir /8.0/cinnamon-extra

 then you are ready to compile the 'cinnamon-extra' collection

    # cd /root/cinnamon
    # bash scripts/cinnamon-extra -s
    # bash scripts/cinnamon-extra -a 

Have fun :)
