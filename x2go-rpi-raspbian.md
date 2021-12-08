[wiki:repositories:raspbian [X2Go - everywhere@home]](https://wiki.x2go.org/doku.php/wiki:repositories:raspbian)

> Please switch to a user which has administrator privileges on your system in your preferred command line client:
> 
> su -
> 
> or
> 
> sudo \-s
> 
> The following command will ensure that your system will be able to work with the repository archive key.
> 
> $ apt-key adv \--recv-keys \--keyserver keys.gnupg.net E1F958385BFE2B6E
> 
> ### Adding the Actual Repository
> 
> Please add the file `x2go.list` to the folder `/etc/apt/sources.list.d/`. This can be done by using your preferred editor.
> 
> If you have not gotten a directory named `/etc/apt/sources.list.d/` add the lines to `/etc/apt/sources.list`.
> 
> $ editor /etc/apt/sources.list.d/x2go.list
> 
> Then add the X2Go repository (binaries and sources) as a couple of new lines (example for Raspbian **buster**):
> 
> [x2go.list](https://wiki.x2go.org/doku.php/wiki:repositories:raspbian?do=export_code&codeblock=4 "Download Snippet")
> 
> \# X2Go Repository (release builds)
> deb http://packages.x2go.org/raspbian buster main
> # X2Go Repository (sources of release builds)
> deb-src http://packages.x2go.org/raspbian buster main
> 
> # X2Go Repository (Saimaa ESR builds)
> #deb http://packages.x2go.org/raspbian buster saimaa
> # X2Go Repository (sources of release builds)
> #deb-src http://packages.x2go.org/raspbian buster saimaa
> 
> # X2Go Repository (nightly builds)
> #deb http://packages.x2go.org/raspbian buster heuler
> # X2Go Repository (sources of nightly builds)
> #deb-src http://packages.x2go.org/raspbian buster heuler
> 
> **Edit this new data** and make sure to uncomment desired components and comment non-desired components. Only one group may be active at a given time.
> 
> While we do offer pseudo-codenames like `oldstable`, `stable`, `testing` and `unstable` for convenience, you **should not use them**. Our pseudo-codename setup is not guaranteed to be in sync with Debian's releases, so using the `stable` codename might mean that you will actually get packages for what Debian calls `oldstable` after a new Debian distro release for a considerable amount of time.
> 
> Switching between components usually requires uninstalling all X2Go packages first! The only upgrade path that is considered somewhat safe is main (release packages) to heuler (nightly packages), but there are no guarantees regarding the stability or usefulness of nightly packages.
> 
> ### Synchronize the Newly Added Repository's Metadata
> 
> Please perform an update of your APT package database:
> 
> $ apt-get update
> 
> If you were unable to bootstrap the repository GPG key previously, apt-get will fail to validate the signatures and discard the downloaded repository metadata.  
>   
> **Not being able to verify signatures means that any content downloaded from the remote location could be injected/offered by a malicious third party and need not come from the X2Go Project. This includes repository metadata and any packages downloaded from unauthenticated repositories. Installing the x2go-keyring package from an unauthenticated repository bears the chance that this is not our package but a malicious third-party one which will not contain our public keys. This holds for all packages installed from this repository, now and later.**  
>   
> You can bypass apt's internal checks **if you understand the implications** and are ready to take the risk by **once** using:  
>   
> 
> $ apt-get update \--allow-insecure-repositories
> 
> Otherwise, please try to first fetch the key again as outlined in the bootstrapping instructions.
> 
> After the update you should be able to access the X2Go packages via the apt command family. As a first action you should install our `x2go-keyring` package and refresh the apt cache:
> 
> $ apt-get install x2go-keyring && apt-get update
> 
> ## Post-Addition Test
> 
> Now you can search for X2Go related packages that are now available for your APT system:
> 
> $ apt-cache search x2go
> 
> Congratulations, you are now able to access the X2Go packages. You may continue by installing x2goserver, x2goclient or pyhoca-gui or any other of the available packages.
> 
> ## Mirroring This Repository
> 
> The packages in this repository can be mirrored via `rsync`:
> 
> rsync -avP packages.x2go.org::raspbian </dest/path/of/local/mirror/raspbian>
