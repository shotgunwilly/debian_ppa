## Creating Debian package instructions:

https://www.iodigital.com/en/history/intracto/creating-debianubuntu-deb-packages

### Build Sample App

Build sample Go app, and place binary in Debian package directory. The file structure in `debian_package` directory represents the target system's root directory. For example, a file placed in `debian_package/usr/local/bin` will be installed on the target system at `/usr/local/bin`. From project root directory:

```
>$ mkdir -p debian-test/usr/local/bin
>$ cd hello_world_app
>$ go build -o ../debian-test/usr/local/bin/hello-debian hello-debian.go
```

### Build Debian Package

Build the Debian package using the following commands:

```
>$ cd ../  \\go to project root directory
>$ dpkg-deb --build debian-test
```

Install Debian package.

```
>$sudo dpkg -i debian-test.deb
```

Linting Debian Package

```
>$ sudo apt install lintian
>$ lintian debian-test.deb 
```

Remove Debian package.

```>$sudo dpkg -r debian-test```


Official Debian Package Guide
https://www.debian.org/doc/manuals/maint-guide/index.en.html


# Creating PPA Repository

Guide used: https://assafmo.github.io/2019/05/02/ppa-repo-hosted-on-github.html

### Creating a GPG key

Create a gpg key using the following commands. Select RSA, then 4096 for key length bits, valid forever for this example, enter contact info, and your key will be created.

```
>$ sudo apt install gnupg
>$ gpg --full-gen-key
```

Create your public key file using the command below. Fill in your email address used to create the gpg key.

```
>$ gpg --armor --export "<EMAIL_ADDRESS>" > path/to/ppa/KEY.gpg
```

Copy Debian packages to ppa folder.

cd ppa
dpkg-scanpackages --multiversion . > Packages
gzip -k -f Packages

Creating the Release, Release.gpg and InRelease files

```
apt-ftparchive release . > Release
gpg --default-key "dude@dude.com" -abs -o - Release > Release.gpg
gpg --default-key "dude@dude.com" --clearsign -o - Release > InRelease
```