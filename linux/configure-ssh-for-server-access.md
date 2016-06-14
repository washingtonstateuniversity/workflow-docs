---
layout: page
title: Configure SSH Locally
---

## Configure local SSH for server access

### OSX

Create an SSH configuration file in your local user directory.

```
touch ~/.ssh/config
```

Open this file and save a configuration similar to the following.

```
Host server-shortname-01
  User username
  Hostname server-long-name-01.web.wsu.edu
  PreferredAuthentication publickey
  IdentityFile ~/.ssh/wsu_private_key_rsa  
```

Multiple configurations can exist in the `~/.ssh/config` directory, usually one per server/username combination.

* `Host` assigns an alias that you'll use at the command line to connect to the server with something like `ssh server-shortname-01`. This is usually easier than typing out the full user, address, and identity file information each time.
* `User` should be the username that you are connecting to on the server.
* `Hostname` is the full URL the alias maps to.
* `IdentityFile` is the private key that was generated when you created a private/public key pair. It should be the corresponding private key to the public key added to the server.

With this configured, `ssh server-shortname-01` will connect as the `username` user to `server-long-name-01.web.wsu.edu`.

### Windows

_Needs Documentation_
