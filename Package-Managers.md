# PACKAGE MANAGERS

Distribution-specific info on different package managers

## ARCH

Pacman for core and community.
AUR for user submitted packages. You can use packages like yay, trizen, pacaur to search and manage.

To make a package from source, download the PKGBUILD file.
    makepkg -si package-name
OR
    makepkg
    pacman -U nameofpackage

Package cache is located at /var/cache/pacman/pkg/

| SWITCH             | DESC                                  |
|--------------------|---------------------------------------|
| -Qs                | search installed packages             |
| -Qq -pipe- wc -l   | list number of packages installed     |
| -Sc                | cleans cache                          |
| -Ql                | list files in package                 |
| yay -Syu           | updates AUR                           |
| -U                 | upgrade/downgrade package             |
| -Qqen > backup.txt | list all installed apps in a document |
| -S $(< backup.txt) | restore backup list                   |

Install the package _pacman-contrib_ to remove all cache except the last 3 versions

    paccache -r

## DEBIAN

| COMMAND                   | DESC                                     |
|---------------------------|------------------------------------------|
| apt-cache search xxx      | search for package                       |
| dpkg -i xxx.deb           | install DEB package                      |
| dpkg -l                   | list all installed packages              |
| apt-mark (un)hold package | hold/unhold package from further updates |
|                           |                                          |

## RED HAT / FEDORA / CENTOS

yum for repo and rpm for local package

create local repository with (install yum-utils)

    yumdownloader

then

    createrepo

local folder for repository info is at /etc/yum.repos.d/. The format for the confg files is:

[repoID]
name=Readable name
baseurl=url://path/to/repo/
file://path/to/localrepo

example (for a repo at /repo):

    vim /etc/yum.repos.d/my.repo
        [myrepo]
        name=My Example Repository
        baseurl=file:///repo
        gpgcheck=0

| COMMAND                           | DESC                                         |
|-----------------------------------|----------------------------------------------|
| yum clean all                     | clean cache                                  |
| yum groups list hidden            | list all available groups                    |
| yum provides */text-to-search     | search in description                        |
| rpm -q xxx                        | search installed packages                    |
| rpm -qd xxx                       | search for documents of package              |
| rpm -qf /etc/file                 | explain which package a file come from       |
| rpm -qa -pipe- grep xxx           | search all installed packages                |
| rpm -qpl rpmfile.rpm              | lists all files that will be installed       |
| rpm -qp --scripts rpmfile.rpm     | similar to PKGBUILD, list scripts in package |
| yum downgrade package.rpm         | downgrade a package                          |
| rpm -Uvh --oldpackage package.rpm | same thing                                   |


## OPENSUSE

Zypper is the package manager.

| SWITCH                     | DESC                                     |
|----------------------------|------------------------------------------|
| update -t package          | updates only selected package            |
| info package               | information about a package              |
| wp package                 | what provides                            |
| addlock                    | lock a package                           |
| lr                         | list repos                               |
| ref                        | refresh                                  |
| in --no-recommends package | install without the recommended software |
| up --no-gpg-checks         | skip integrity check                     |
| dup                        | distribution upgrade                     |













z
