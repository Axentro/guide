## What is config for

Config can be used with all the binaries and provides a shortcut when using the command line. Consider this example:

```bash
> axe tx create -m 5 -f 0.0001 -w wallets/w1.json -n http://testnet.axentro.io:3000 -a some-address --testnet --password=password
```

For every command you have to specify several command line options. Config can save these so you don't have to pass them everytime and instead if not passed they are retrieved from the config store. If any of the options are provided on the command line then they override any previously stored config options.

This provides a very easy to use and flexible configuration solution. The above command could be shortened using config to this:

```bash
> axe tx create -m 5 -f 0.0001 -a some-address
```

we think you will agree that is much easier to work with.

## Usage

There are 7 things you can do with config:

```
available sub actions
 - save                 | save the specified options as default for axe, axen and axem
 - show                 | show current default configuration
 - remove               | remove the default configuration
 - use                  | use the specified configuration
 - list                 | list the available configurations
 - enable               | enable configurations
 - disable              | disable configurations
```

In addition to those usages you can also override config completely - which is very hand if you have saved config for different things e.g

```bash
> axen --config=myserver1
> axem -c myminer1
> axe wallet amount -c wallet1
```

### Save

Save stores the specified config to the location: `~/.axentro/config`. You just have to supply the config you would like to save and a config name to save it under (the default name is config which is used if no name is supplied):

```bash
> axe config save -n http://testnet.axentro.io:3000 --testnet --config=myconfig
```

### Show

You can view the list of stored config using the show command:

```bash
> axe config show
```
```
current configuration is for: 's1t' in file /Users/kings/.axentro/config
configuration is Enabled
--------------------
connect_node:	http://testnet.axentro.io:3000
wallet_path:	/Users/kings/sc-wallets/w1.json
is_testnet:	true
is_private:	true
bind_host:	0.0.0.0
bind_port:	3000
processes:	1
encrypted:	false
```

### Remove

If you want to remove a specific configuration or all configurations (this will delete the config file)

```bash
> axe config remove --config=myconfig
> axe config remove
```

### Use

If you want to switch to using a different default config:

```bash
> axe config use --config=myconfig
```

### List

To see a list of all the saved configs

```bash
> axe config list
```

### Enable / Disable

If you want to completely disable configurations so they don't apply or turn them back on again:

```
> axe config disable
> axe config enable
```

## Supported config

The following config can be saved:

| Option name     | Flag        | binary |
| --------------- | ----------- | ------ |
| Connecting node | -n          | all    |
| Wallet path     | -w          | all    |
| Wallet password | --password= | all    |
| Is testnet      | --testnet   | all    |
| Is private      | --private   | axen   |
| Bind host       | -h          | axen   |
| Bind port       | -p          | axen   |
| Public url      | -u          | axen   |
| Database path   | -d          | axen   |
| Threads         | --threads=  | axem   |
| Encrypted       | -e          | axe    |

