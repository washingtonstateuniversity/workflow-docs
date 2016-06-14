---
layout: page
title: Generate a Key Pair
---

## Generate a local private/public key pair for authentication

### OSX

```
ssh-keygen -t rsa -b 4096 -C "user@example.org"
```

Enter a file location when requested. It's okay to accept the default suggestion, though it can be useful to generate a new private/public key pair for each server or application. If you'd like to do this, use a full filename such as `/Users/username/.ssh/new_key_name_rsa`.

```
Enter file in which to save the key (/Users/username/.ssh/id_rsa):
```

This will generate two files in `/Users/username/.ssh/`, `new_key_name_rsa` (the private key) and `new_key_name_rsa.pub` (the public key). Your next step will likely be to open `new_key_name_rsa.pub` and copy its contents so that it can be used elsewhere. Do not share the private key, it should remain on your machine.

### Windows

_Needs Documentation_
