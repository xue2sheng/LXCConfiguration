# LXC Configuration

Draft notes on how to configure [LXC](https://linuxcontainers.org) on different platforms than the obvious [Ubuntu LXD](https://www.ubuntu.com/containers/lxd).

The host Linux will be one [TumbleWeed openSUSE](https://en.opensuse.org/Portal:Tumbleweed) and one [Debian Sid](https://www.debian.org/releases/sid/) that work as **rolling release** and got latest *Kernel* versions. It'd be a good idea to give it a shot to [ArchLinux](https://www.archlinux.org) as well.

## openSUSE

Provided you got already intalled *lxc*, i.e. "sudo zypper install lxc", let's have a look to:

### Installing latest GO

Instead of relying only on raw scriptin, [latest Go](https://github.com/moovweb/gvm) *- a compiled, garbage-collected, concurrent programming language -* is expected to be installed.

You need a working verson of *go* in order to build its latest version:

    sudo zypper install go ## stock version
    export GOROOT_BOOTSTRAP=/usr/lib64/go
    bash < <(curl -s -S -L https://raw.githubusercontent.com/moovweb/gvm/master/binscripts/gvm-installer)
    source "/home/user/.gvm/scripts/gvm"
    gvm listall ## choose latest version
    gvm install go1.8
    gvm use go1.8 --default
    sudo zypper remove go go-doc ## no longer needed stock version
    
### Installing latest LXD

That step might be NOT the best idea if you plan to **learn** LXC but I must admit using **[LXD](https://github.com/lxc/lxd)**, *- a daemon based on liblxc offering a REST API to manage containers -*, on Ubuntu has spoilt me ;)

#### Build LXD

    sudo zypper install acl dnsmasq dnsmasq-utils git lxc lxcfs liblxc-devel liblxc1 libvirt-deamon-driver-lxc libvirt-deamon-lxc  make pkg-config rsync squashfs tar xz xz-devel lvm2 lvm2-devel libbtrfs-devel btrfsprogs curl gettext-runtime gettext-tools jq sqlite3 uuidd uuid-devel libuuid1 python-pyflakes python-pep8 bzr ShellCheck
    go get github.com/lxc/lxd
    cd $GOPATH/src/github.com/lxc/lxd
    make
    
#### Access to its source code for possible additional fixes

    cd ~ && mkdir -p Code && cd Code
    git clone https://github.com/lxc/lxd.git
    
#### LXD Machine Setup

You'll need sub{u,g}ids for root, so that LXD can create the unprivileged containers:

    echo "root:1000000:65536" | sudo tee -a /etc/subuid /etc/subgid

Now you can run the daemon (the --group sudo bit allows everyone in the sudo group to talk to LXD; you can create your own group if you want):

    sudo -E $GOPATH/bin/lxd --group sudo
    
 ## Hello, World!
 
 Taking for granted you're following previous links to [LXC](https://linuxcontainers.org) and to [LXD](https://github.com/lxc/lxd), there's nothing to write home in the following commands:
 
 
