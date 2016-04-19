# Installing pkgsrc from http://pkgsrc.joyent.com/


## Getting and Installing pkgin/pkgsrc

### 64-bit

```
: Download 64-bit bootstrap kit
$ curl -Os https://pkgsrc.joyent.com/packages/SmartOS/bootstrap/bootstrap-2015Q3-x86_64.tar.gz

: Verify SHA1 checksum
$ /bin/digest -a sha1 bootstrap-2015Q3-x86_64.tar.gz
65372cf50f580fa19a8a6a24464349f0d61b99d6

: Verify PGP signature (optional, requires gpg) # I haven't quite figured this one out on OpenIndiana yet.
$ curl -Os https://pkgsrc.joyent.com/packages/SmartOS/bootstrap/bootstrap-2015Q3-x86_64.tar.gz.asc
$ gpg2 --recv-keys 0xDE817B8E
$ gpg2 --verify bootstrap-2015Q3-x86_64.tar.gz{.asc,}

: Install bootstrap kit to /opt/local
$ sudo tar -zxpf bootstrap-2015Q3-x86_64.tar.gz -C /

: Add to PATH/MANPATH
$ PATH=/opt/local/sbin:/opt/local/bin:$PATH
$ MANPATH=/opt/local/man:$MANPATH
```

### 32-bit

```
: Download 32-bit bootstrap kit
$ curl -Os https://pkgsrc.joyent.com/packages/SmartOS/bootstrap/bootstrap-2015Q3-i386.tar.gz

: Verify SHA1 checksum
$ /bin/digest -a sha1 bootstrap-2015Q3-i386.tar.gz
430800a5221b9608b7ead8dbd6bf316b79c0ab8f

: Verify PGP signature (optional, requires gpg) # I haven't quite figured this one out on OpenIndiana yet.
$ curl -Os https://pkgsrc.joyent.com/packages/SmartOS/bootstrap/bootstrap-2015Q3-i386.tar.gz.asc
$ gpg2 --recv-keys 0xDE817B8E
$ gpg2 --verify bootstrap-2015Q3-i386.tar.gz{.asc,}

: Install bootstrap kit to /opt/local
$ sudo tar -zxpf bootstrap-2015Q3-i386.tar.gz -C /

: Add to PATH/MANPATH
$ PATH=/opt/local/sbin:/opt/local/bin:$PATH
$ MANPATH=/opt/local/man:$MANPATH
```

### Multiarch

I haven't tested this myself, but I assume it ***should*** work.

```
: Download multiarch bootstrap kit
$ curl -Os https://pkgsrc.joyent.com/packages/SmartOS/bootstrap/bootstrap-2015Q3-multiarch.tar.gz

: Verify SHA1 checksum
$ /bin/digest -a sha1 bootstrap-2015Q3-multiarch.tar.gz
5da107efba21840d957227bf568f5df5e86b534d

: Verify PGP signature (optional, requires gpg) # I haven't quite figured this one out on OpenIndiana yet.
$ curl -Os https://pkgsrc.joyent.com/packages/SmartOS/bootstrap/bootstrap-2015Q3-multiarch.tar.gz.asc
$ gpg2 --recv-keys 0xDE817B8E
$ gpg2 --verify bootstrap-2015Q3-multiarch.tar.gz{.asc,}

: Install bootstrap kit to /opt/local
$ sudo tar -zxpf bootstrap-2015Q3-multiarch.tar.gz -C /

: Add to PATH/MANPATH
$ PATH=/opt/local/sbin:/opt/local/bin:$PATH
$ MANPATH=/opt/local/man:$MANPATH
```

## Post-Install Steps

### Use pkgin to install packages

```pkgin``` is the front-end to the binary packages, and lets you search for, install, upgrade, and remove packages. It also provides some basic functionality for querying both local and remote packages. If you have used ```apt-get``` or ```yuml youckaging tools are pkg_add, pkg_admin, pkg_create, pkg_delete, and pkg_info. If pkgin is equivalent to apt-get or yum, then these are the equivalent of dpkg or rpm. Here are some useful commands to get you started.should find it to be very familiar.


You'll need to run ```sudo pkgin -y update``` first before you can do searches.

```
: Search for a package.  Regular expressions are supported.
$ pkgin search "^ffmpeg[12]*$"
ffmpeg2-2.6          Decoding, encoding and streaming software (v2.x)
ffmpeg1-1.2.12       Decoding, encoding and streaming software (v1.x)

: Install a package without prompting
$ sudo pkgin -y install ffmpeg2

: List all available packages
$ pkgin avail

: Refresh the pkgin database with the latest version
$ sudo pkgin -y update

: Upgrade all out-of-date packages
$ sudo pkgin -y full-upgrade

: Remove a package
$ sudo pkgin -y remove ffmpeg2

: Automatically remove orphaned dependencies
$ sudo pkgin -y autoremove
```

### Use pkg_* tools to manage packages

The underlying packaging tools are ```pkg_add```, ```pkg_admin```, ```pkg_create```, ```pkg_delete```, and ```pkg_info```. If ```pkgin``` is equivalent to ```apt-get``` or ```yum```, then these are the equivalent of ```dpkg``` or ```rpm```. Here are some useful commands to get you started.

```
: See what packages are installed.
$ pkg_info

: See what package a file belongs to.
$ pkg_info -Fe /opt/local/bin/node
nodejs-0.12.2

: List the contents of a package.
$ pkg_info -qL nodejs
/opt/local/bin/node
/opt/local/bin/npm
[...]

: Perform an audit of all currently installed packages.
$ sudo pkg_admin fetch-pkg-vulnerabilities
$ pkg_admin audit
Package openssl-1.0.1i has a multiple-vulnerabilities vulnerability, see https://www.openssl.org/news/secadv_20141015.txt
Package python27-2.7.8 has a arbitrary-code-execution vulnerability, see http://bugs.python.org/issue22885
[...]

: Create a binary package from some metadata files and package directory.
$ pkg_create -B build-info -c comment -d description -f packlist -I /opt/local -p files/ -U foo-1.0.tgz
```

All these docs are mainly sourced from http://pkgsrc.joyent.com/install-on-illumos/ and credit goes to https://pkgsrc.joyent.com !
