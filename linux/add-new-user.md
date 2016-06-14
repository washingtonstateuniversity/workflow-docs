---
layout: page
title: Add New Users
---

## Add a new user to a server

### Create the user

Create the user with the `ucadmin` group and then assign `www-data` as a secondary group.

```
cd /home/
adduser username -g ucadmin -m
usermod -a -G www-data username
```

### Setup the user account with a public key for authentication

Create a `.ssh` directory in the user's home directory. Make sure it is owned by the user (`chown`) and only accessible by the user (`chmod 700`).

```
mkdir /home/username/.ssh
cd /home/username/
chown username:ucadmin /home/username/.ssh
chmod 700 /home/username/.ssh
```

Create an `authorized_keys` file in the user's `.ssh` directory. Make sure it is owned by the user (`chown`) and only accessible by the user (`chmod 600`).

```
cd /home/username/.ssh
touch authorized_keys
chown username:ucadmin authorized_keys
chmod 600 authorized_keys
```

Open the `authorized_keys` file and paste the entirety of the user's generated public key that will be used for authentication.

```
vi authorized_keys
```

Set a strong, temporary password for the user and pass that to them with SSH configuration instructions.

```
passwd username
```
