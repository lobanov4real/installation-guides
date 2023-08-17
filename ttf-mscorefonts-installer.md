# Script for download and install mscorefonts for Linux

The script searches the Debian repository for the latest deb package for Microsoft fonts, downloads the latest version to the /tmp directory, and initiates the installation of the downloaded package.

## Create bash-scripts

```shell
vi ~/mscorefonts.sh
```

```shell
# !/bin/bash

# Get the latest deb package link using curl and grep

deb_link=$(curl -s <http://ftp.us.debian.org/debian/pool/contrib/m/msttcorefonts/> | grep -oE 'href="ttf-mscorefonts-installer_[^"]*\.deb"' | sort -Vr | head -n 1 | cut -d'"' -f2)

# If a deb package link was obtained successfully

if [ -n "$deb_link" ]; then
    # Form the complete link to the latest deb package
    full_deb_link="<http://ftp.us.debian.org/debian/pool/contrib/m/msttcorefonts/$deb_link>"

    # Download the latest deb package to the /tmp/ directory
    wget $full_deb_link -P /tmp/

    echo "Downloaded deb package: $full_deb_link"

    # Install the deb package from /tmp/ with automatic confirmation
    sudo dpkg -i /tmp/$(basename $deb_link) -y
else
    echo "Failed to obtain the link to the latest deb package."
fi
```

## Run scripts

Run scrips with sudo to avoid interactive message during installation process:

```shell
sudo sh ~/mscorefonts.sh
```
