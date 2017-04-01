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
    
    

