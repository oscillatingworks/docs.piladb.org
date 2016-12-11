# Installation

The process of installing **piladb** might differ depending on your role and purposes.

## For users 🙋

As a user of **piladb** you only need a HTTP client that lets interact with the REST API database server, `pilad`. This a list of some of the most popular HTTP clients out there:

* Command line interface: [`curl`](https://curl.haxx.se/), [`httpie`](https://httpie.org/).
* Graphical user interface:
  * [Insomnia](https://insomnia.rest/) (Linux, Mac, Windows)
  * [Paw](https://paw.cloud/) (Mac)
  * [Postman](https://www.getpostman.com/) (web, Mac)
* Programming languages: Every language should have a solid HTTP client that lets you interact programatically with **piladb**. A simple web search should point you into the right direction. For example, [HTTP clients for Ruby](http://lmgtfy.com/?q=ruby+http+client).

## For admins 🤓

As an admin, you want to manage `pilad`, the **piladb** server. In order to do that, you can choose one of the following approaches:

### Releases

> Requirements: `unzip` or `tar` command line tools.

All official **piladb** releases are hosted on Github. Find the latest release for your platform and architecture in [the Downloads list at the release page](https://github.com/fern4lvarez/piladb/releases/latest). They are available on `zip` and `tar.gz` formats.

#### zip

```basg
unzip piladb_OS_ARCH.zip
```

#### tar.gz

```bash
tar -zxvf piladb_OS_ARCH.tar.gz
```

When you uncompress the file, you will find inside the resulting directory a `pilad` binary file. Set execution permissions to the file  with `chmod +x pilad`. Now you can move the binary file wherever you need. For more about `pilad` usage, go to the next page.

### Go installer

> Requirements: [Go](https://golang.org/dl/) +1.6 installed and `GOPATH` setup.

Download and install the project with:

```bash
go get -u github.com/fern4lvarez/piladb/...
```

You will find the `pilad` binary file into `$GOPATH/bin` with the right permissions and full compatibility with the host.

### Docker

> Requirements: [Docker](https://www.docker.com/products/overview) installed.

You can execute `pilad` from a Docker container, so you don't make a manual installation or depend on Go. With Docker configured, execute:

```bash
docker run -d --name piladb -p $PILADB_PORT:1205 fern4lvarez/piladb
# -d: start container in the background as a daemon
# --name: give a name to the container
# -p: `pilad` will listen on `$PILADB_PORT` from outside of the container
# fern4lvarez/piladb es el nombre oficial de la imagen 
```

This will bootstrap a `pilad` instance, listening on a the Port number set with `$PILADB_PORT`.









