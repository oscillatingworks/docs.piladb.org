# Installation

The process of installing **piladb** might differ depending on your role and purposes.

> Before installing **piladb**, please consider that it was designed and developed from **Linux** for **Linux**. Although, compatibility and first class support for **Mac** is guaranteed, and it will stay like this forever. Said this, **piladb** should work on platforms like **Windows** or ***BSD** too, yet there's not official support as of now.


## For users 🙋

As a user of **piladb** you only need a HTTP client that makes it possible to interact with the REST API of the database server, `pilad`. This a list of some of the most popular HTTP clients out there:

* Command line interface: [`curl`](https://curl.haxx.se/), [`httpie`](https://httpie.org/).
* Graphical user interface:
  * [Insomnia](https://insomnia.rest/) (Linux, Mac, Windows)
  * [Paw](https://paw.cloud/) (Mac)
  * [Postman](https://www.getpostman.com/) (web, Mac)
* Programming languages: Every language should have a solid HTTP client that lets you interact programatically with **piladb**. A simple web search should point you into the right direction. For example, [HTTP clients for Ruby](http://lmgtfy.com/?q=ruby+http+client).

## For admins 💻

As an admin, you want to manage `pilad`, the **piladb** server. In order to do that, you can choose one of the following approaches:

### Releases

> Requirements: `unzip` or `tar` command line tools.

All official **piladb** releases are hosted on Github. Find the latest release for your platform and architecture in [the Downloads list at the releases page](https://github.com/fern4lvarez/piladb/releases/latest). They are available on `zip` and `tar.gz` formats.

#### zip

```bash
unzip piladbX.Y.Z.OS-ARCH.zip
```

#### tar.gz

```bash
tar -zxvf piladbX.Y.Z.OS-ARCH.tar.gz
```

When you uncompress the file, you will find inside the resulting directory a `pilad` binary file. Move the binary file where you want to execute it from. For more about `pilad` usage, go to the next page.

### Go installer

> Requirements: `git` and [Go](https://golang.org/dl/) +1.6 installed, and `GOPATH` setup.

Download and install the project with:

```bash
go get -u github.com/fern4lvarez/piladb/...
```

You will find the `pilad` binary file into `$GOPATH/bin` with the right permissions and full compatibility with the host.

### Docker

> Requirements: [Docker](https://www.docker.com/products/overview) installed.

You can execute `pilad` from a Docker container, so you don't to install or depend on Go. With Docker configured, execute:

```bash
docker run -d --name piladb -p $PILADB_PORT:1205 fern4lvarez/piladb
# -d: start container in the background as a daemon
# --name: give a name to the container
# -p: `pilad` will listen on `$PILADB_PORT` from outside of the container
# fern4lvarez/piladb is the official name of the image
```

This will bootstrap a `pilad` instance, listening on a the Port number set with `$PILADB_PORT`.

## For Developers 🔧

> Requirements: `git` and [Go](https://golang.org/dl/) +1.6 installed, and `GOPATH` setup.

If you want to develop or play with **piladb** you need to download the source code using Go:

```bash
go get -u github.com/fern4lvarez/piladb/...
cd $GOPATH/src/github.com/fern4lvarez/piladb
```

Then you can run `make all` to check that everything is OK. Take a look at the [`README.md`](https://github.com/fern4lvarez/piladb/blob/master/README.md) file, as it contains useful and important information for developers.

### The Docker way

> Requirements: `git` and [Docker](https://www.docker.com/products/overview) installed.

If you don't have or want Go installed in your machine, take the Docker way. This is not only valid for running `pilad` from a container as we've seen previously, but also to provide a development environment where you can work without modifying your host machine.

The container comes with `vim` and `git` preinstalled, which is what you might need for basic development. Run this steps to get a dev setup up and running:

```bash
git clone https://github.com/fern4lvarez/piladb.git
cd piladb
cd dev
make run  # will start piladb container
make bash  # connect into the container
```

You are in! Now run `ls -al`, `vim` or `make all` to check that you have indeed all you need inside the container.













