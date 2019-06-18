# Depho

[![](https://img.shields.io/badge/license-GPLv3+-blue.svg?style=flat-square)](LICENSE)


## About

Depho lets you deploy a directory on remote servers as your `HOME` directory on
demand before you log into this server via SSH. This can be very useful to keep
configuration files up to date without using a shared storage, i.e. for servers
in remote data centers.


## Usage

Using `depho` is really easy. Just download the script, add an alias in your
`.bashrc` and define the target directory on the remote host:

```
alias ssh='/path/to/depho'
export DEPHO_TARGET=/tmp/roaming
```

`depho` can be configured by setting these variables in the environment:

* `DEPHO_SOURCE`:

  The directory `depho` is syncing to the remote server. Defaults to
  `$HOME/.ssh/depho`.

* `DEPHO_TARGET`:

  The target directory, where the synced data is stored at the remote host.

  *NOTE: The target directory needs to be unique to identify the user at the
  remote host. Otherwise the contents of different users may conflict.*

  *NOTE: The target directory should reside in a temporary location (i.e.
  `/tmp`), as the target directory will NOT be removed after logout, but should
  be removed on reboots of the remote hosts.*

* `DEPHO_SHELL`:

  The shell to be used. Defaults to `/bin/bash`.

* `DEPHO_HOSTS`:

  An optional list of hosts to be whitelisted. Defaults to
  `$HOME/.ssh/depho.hosts`.


### Host whitelist

By default all hosts will be provisioned by `depho`. However, if a host
whitelist file is available, the hosts will be checked against this whitelist.
Hosts not matching the whitelist will be ignored by `depho` and the command just
pass through to the native SSH client.

*NOTE: As the whitelist will be checked by `grep`, regular expressions
can be used.*


## License

This project is licensed under the [GPLv3+](LICENSE).

&copy; 2019 mksec, Alexander Haase
