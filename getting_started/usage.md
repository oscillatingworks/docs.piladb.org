# How to use piladb?

Now that you know [how to install **piladb**](installation.md) and what do you need to start using it, let's do real things with it. We will start a `pilad` server and play with it. You don't need to understand all of the steps, copy-pasting the steps in your terminal and checking the output will be enough for now.

## Start the server

If you followed correctly the [Installation](installation.md) instructions as an admin, you should have access to the `pilad` binary:

```
pilad -h
```

Do you see the Usage of `pilad` as an output? Then you are fine. `pilad` provides some configuration flags, but we'll stick with the defauls for now. Let's start the server for real:

```
pilad
```

This will show you the logs in your terminal. Something like this:

```
2014/05/12 23:24:03 
2014/05/12 23:24:03          d8b 888               888 888      
2014/05/12 23:24:03          Y8P 888               888 888      
2014/05/12 23:24:03              888               888 888      
2014/05/12 23:24:03 88888b.  888 888  8888b.   .d88888 88888b.  
2014/05/12 23:24:03 888 "88b 888 888    "88b  d88" 888 888 "88b 
2014/05/12 23:24:03 888  888 888 888 .d888888 888  888 888  888 
2014/05/12 23:24:03 888 d88P 888 888 888  888 Y88b 888 888 d88P 
2014/05/12 23:24:03 88888P"  888 888 "Y888888  "Y88888 88888P"  
2014/05/12 23:24:03 888
2014/05/12 23:24:03 888
2014/05/12 23:24:03 888
2014/05/12 23:24:03 
2014/05/12 23:24:03 Version: 1b8b3972367f6f1c5ea439e0236c84ff5ac3f16c
2014/05/12 23:24:03 Host:    linux_amd64
2014/05/12 23:24:03 Port:    1205
2014/05/12 23:24:03 PID:     572
2014/05/12 23:24:03 
```

Keep an eye on this output, as it will log all activities processed by `pilad`.

> 🔝 **_Protip!_** You can log into a file with `pilad &> pilad.log &`

## Play with piladb

> We will use `curl` for this walkthrough. You can use your favorite HTTP client, considering that some options might change.

So now `pilad` is running on `localhost:1205`. If we access the root page will be redirected to the official `pilad` REST API documentation:

```bash
curl -L localhost:1205
# -L follow redirects
```

We can also check the current status of **piladb**:

```bash
curl localhost:1205/_status
```

Or the current configuration values:

```bash
curl localhost:1205/_config
```

### Create a Database

To start working with **piladb**, we need to create a new _Database_, which  will contain the _Stacks_ we will work with:

```bash
curl -XPUT localhost:1205/databases?name=MY_DATABASE
```

We will see the new _Database_ as an output in JSON format. We can have access to this content everytime by requesting the new _Database_ itself:

```bash
curl localhost:1205/databases/MY_DATABASE
```

```json
{
  "number_of_stacks": 0,
  "name": "MY_DATABASE",
  "id": "da5bf1684cdb20bd0be0b767007b9e82"
}
```

> 🔝 **_Protip!_** Install [`jq`](https://stedolan.github.io/jq/) to print and process the JSON responses.

Also, we can list all existing databases:

```bash
curl localhost:1205/databases
```

```json
{
  "databases": [
    {
      "number_of_stacks": 0,
      "name": "MY_DATABASE",
      "id": "da5bf1684cdb20bd0be0b767007b9e82"
    }
  ],
  "number_of_databases": 1
}
```







