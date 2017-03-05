# Clients

This a list and description of the officially supported clients for **piladb**. For more information, please visit the repository of each of them.

## Shell

The [shell client](https://github.com/oscillatingworks/piladb-sh) is more like a set of utilities around **piladb** rather than a client library as usual. `piladb.sh`is a shell script that contains functions that will be exported into your shell as commands, as well as an API for your shell scripts. They are compatible with `bash` and `zsh`, and can be installed with a single command:

```bash
source <(curl -s https://raw.githubusercontent.com/oscillatingworks/piladb-sh/master/piladb.sh)
```

Now if you type `piladb_help` you can see a summary of all new available commands. With these commands you can:

* Download and install `pilad` binary: `piladb_download`.
* Start and stop a `pilad` local server: `piladb_start`, `piladb_stop`.
* Create, show and delete Databases: `piladb_create_database $database_name`, `piladb_show_databases`, `piladb_show_database $database_name`, `piladb_delete_database $database_name`.
* Create show and delete Stacks: `piladb_create_stack $database_name $stack_name`, `piladb_show_stacks $database_name`, `piladb_show_stack $database_name $stack_name`, `piladb_delete_stack $database_name $stack_name`.
* Operations in Stacks: `piladb_PUSH $database_name $stack_name $element`, `piladb_{POP,PEEK,SIZE,FlUSH} $database_name $stack_name`.
* Show Status of piladb: `piladb_status`.
* Show, get or set a Config value: `piladb_config`, `piladb_config_get $config_key`, `piladb_config_set $config_key config_value`.

[HTTPie](https://httpie.org/) is used as HTTP client under the hood, so it is a requirement in order to use most of these commands. If you find a bug or you want to contribute, feel free to open an Issue or Pull Request in the [Github repo](https://github.com/oscillatingworks/piladb-sh/issues/new).

## Go

Not implemented. [Help!](https://github.com/oscillatingworks/piladb-go)

## Ruby

Not implemented. [Help!](https://github.com/oscillatingworks/piladb-rb)

## JavaScript

Not implemented. [Help!](https://github.com/oscillatingworks/piladb-js)
