[doc:installation:x2goserver [X2Go - everywhere@home]](https://wiki.x2go.org/doku.php/doc:installation:x2goserver)

> ## Ubuntu
> 
> ### Quick
> 
> You might have to install `add-apt-repository` first.
> 
> To install `add-apt-repository` on Ubuntu 10.04 or 12.04:
> 
> sudo apt-get install python-software-properties
> 
> To install `add-apt-repository` on Ubuntu 14.04:
> 
> sudo apt-get install software-properties-common
> 
> Once `add-apt-repository` is installed, run these commands:
> 
> sudo add-apt-repository ppa:x2go/stable
> sudo apt-get update
> sudo apt-get install x2goserver x2goserver-xsession
> 
> ### Detailed
> 
> First add the [X2Go ppa repository for Ubuntu](https://wiki.x2go.org/doku.php/wiki:repositories:ubuntu "wiki:repositories:ubuntu").
> 
> After adding the X2Go PPA to your remote Ubuntu “desktop” server the next step is to install the packages `x2goserver` and `x2goserver-xsession`:
> 
> sudo apt-get install x2goserver x2goserver-xsession
> 
> ## Debian
> 
> Add our [X2Go Debian Repository](https://wiki.x2go.org/doku.php/wiki:repositories:debian "wiki:repositories:debian").
> 
> sudo apt-get install x2goserver x2goserver-xsession
> 
> ## Raspbian
> 
> Add our [X2Go Raspbian Repository](https://wiki.x2go.org/doku.php/wiki:repositories:raspbian "wiki:repositories:raspbian").
> 
> sudo apt-get install x2goserver x2goserver-xsession
> 
> ## Gentoo
> 
> Currently X2Go cannot connect to an openssh server compiled with the HPN patch. To make sure x2goserver works on your Gentoo server, you must recompile net-misc/openssh with HPN support disabled. Add the following line to /etc/portage/packages.use:
> 
> net-misc/openssh -hpn
> 
> Then recompile net-misc/openssh, update the configuration file, and restart the sshd server, as follows:
> 
> emerge -1 net-misc/openssh
> dispatch-conf
> /etc/init.d/sshd restart
> 
> Then, install `net-misc/x2goserver`.
> 
> ## Fedora 19 and later
> 
> No additional repositories required:
> 
> sudo yum install x2goserver
> 
> ## RHEL 7
> 
> Add the EPEL repository:
> 
> [EPEL Installation Intructions](https://fedoraproject.org/wiki/EPEL#How_can_I_use_these_extra_packages.3F "https://fedoraproject.org/wiki/EPEL#How_can_I_use_these_extra_packages.3F")
> 
> Check that you have activated the “optional” channel:
> 
> sudo subscription-manager repos \--list
> 
> If the optional channel for your base channel is not active, activate it.
> 
> sudo subscription-manager repos \--enable\=rhel-7\-server-optional-rpms
> 
> Or use the RHNS web interface to activate the channel “RHEL Server Optional”
> 
> Then
> 
> sudo yum install x2goserver x2goserver-xsession
> 
> ## RHEL 6
> 
> There are two sources for X2Go packages for RHEL 6 - our packages repository and Fedora EPEL.
> 
> Select **one method only** and follow [adding X2Go to RedHat-based systems](https://wiki.x2go.org/doku.php/wiki:repositories:epel "wiki:repositories:epel") to configure the repository of your choice.
> 
> ### Activating Optional Channels for RHEL
> 
> Check that you have activated the “optional” channel:
> 
> sudo rhn-channel \-l
> 
> If the optional channel for your base channel is not active, activate it.
> 
> sudo rhn-channel \--add \-c rhel-x86\_64-server-optional-6
> 
> ### Installing sshfs (fuse)
> 
> Currently, even in the optional channel, there is no official package for sshfs and it is not (yet?) included in the X2Go repo. Thus it has to be downloaded form an alternate source:
> 
> #### Option 1: Download the package manually
> 
> sudo yum install fuse fuse-libs
> wget http://pkgs.repoforge.org/fuse-sshfs/fuse-sshfs-2.2\-1.el6.rf.x86\_64.rpm
> sudo rpm \-i \--nosignature fuse-sshfs-2.2\-1.el6.rf.x86\_64.rpm
> 
> #### Option 2: Install EPEL
> 
> URL to most recent EPEL repo installation package available [here](http://mirror01.th.ifl.net/epel/6/i386/repoview/epel-release.html "http://mirror01.th.ifl.net/epel/6/i386/repoview/epel-release.html")
> 
> wget http://mirror01.th.ifl.net/epel/6/i386/epel-release-6\-7.noarch.rpm
> sudo rpm \-i epel-release-6\-7.noarch.rpm
> sudo yum install fuse-sshfs
> 
> ### Installing X2Go Server
> 
> You should now be able to install the `x2goserver` package:
> 
> sudo yum install x2goserver
> 
> if you are installing from EPEL6 or EPEL7, install the `x2goserver-xsession` package also:
> 
> sudo yum install x2goserver-xsession
> 
> ## EPEL 5 (via packages.x2go.org)
> 
> Due to [bug #714](http://bugs.x2go.org/cgi-bin/bugreport.cgi?bug=714 "http://bugs.x2go.org/cgi-bin/bugreport.cgi?bug=714"), currently yum will not tell you what is needed.
> 
> [Add the X2Go repo](https://wiki.x2go.org/doku.php/wiki:repositories:epel "wiki:repositories:epel") to your yum configuration by following the steps on that page.
> 
> ### Installing Required Dependencies (fuse and perl modules)
> 
> #### Download required packages manually
> 
> One approach is to download required packages manually. Yum will tell you what is needed, when you ask it to install `x2goserver`.
> 
> -   perl(DBI::db) - [perl-DBI-1.615-2.x86\_64.rpm](http://flexbox.sourceforge.net/centos/5/x86_64/perl-DBI-1.615-2.x86_64.rpm "http://flexbox.sourceforge.net/centos/5/x86_64/perl-DBI-1.615-2.x86_64.rpm")
>     
> -   perl(File::BaseDir) - perl-File-BaseDir-0.03-1.el5.noarch.rpm
>     
> -   perl(Sys::Syslog) - perl-Sys-Syslog-0.27-1.el5.x86\_64.rpm
>     
> -   fuse - fuse-2.7.4-8.el5.x86\_64.rpm
>     
> -   libfuse.so.2 - fuse-libs-2.7.4-8.el5.x86\_64.rpm
>     
> -   fuse-sshfs - fuse-sshfs-2.2-1.el5.rf.x86\_64.rpm
>     
> 
> -   `rpm -i –nosignature perl-DBI-1.615-2.x86_64.rpm perl-File-BaseDir-0.03-1.el5.noarch.rpm perl-Sys-Syslog-0.27-1.el5.x86_64.rpm`
>     
> -   `rpm -i –nosignature fuse-sshfs-2.2-1.el5.rf.x86_64.rpm fuse-libs-2.7.4-8.el5.x86_64.rpm fuse-2.7.4-8.el5.x86_64.`
>     
> 
> ### Installing X2Go Server
> 
> You should now be able to install the `x2goserver` & `x2goserver-xsession` packages:
> 
> yum install x2goserver
> 
> ## SUSE
> 
> Follow the the instructions for [X2Go Packages for SUSE-Based Systems](https://wiki.x2go.org/doku.php/wiki:repositories:suse "wiki:repositories:suse") to add appropriate repositories.
> 
> ### Installing X2GoServer
> 
> zypper install x2goserver
> 
> ### Workaround for Qt-based Applications and sudo/kdesu
> 
> Please keep this section in sync with the README.sudoers file in our packages!
> 
> #### Problem Description
> 
> OpenSUSE 11 and SLES/SLED 11 do not support /etc/sudoers.d as a place for custom sudoers config files.
> 
> If you are using any of these distributions and are having issues regarding running Qt applications with elevated privileges (e.g., via kdesu or sudo), please use this workaround.
> 
> #### Necessary Actions
> 
> 1.  Copy the contents of the “x2goserver” file residing in the documentation directory `/usr/share/doc/packages/x2goserver`.
>     
> 2.  Get elevated privileges. Either via
>     
>     su
>     
>     or
>     
>     sudo \-i
>     
> 3.  Launch
>     
>     visudo
>     
> 4.  Paste the previously copied content at the end of the sudoers file.
>     
> 5.  Save and exit your editor.
>     
> 
> ## Arch Linux
> 
> `x2goserver` is available in the `extra` repo.
> 
> See [https://wiki.archlinux.org/index.php/X2Go](https://wiki.archlinux.org/index.php/X2Go "https://wiki.archlinux.org/index.php/X2Go") fore more info.
> 
> ## Slackware
> 
> SlackBuilds for `x2goserver` are available on SlackBuilds.org:
