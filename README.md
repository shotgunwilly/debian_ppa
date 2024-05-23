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

```>$sudo dpkg -i debian-test.deb```

Remove Debian package.

```>$sudo dpkg -r debian-test```


Official Debian Package Guide
https://www.debian.org/doc/manuals/maint-guide/index.en.html
