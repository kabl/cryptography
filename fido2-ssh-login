# FIDO2 SSH Login

SSH Login with FIDO2 authentication. Such as YubiKey or SoloKey devices and more.

## Prerequisites

- Requires OpenSSH_8.2p1 or higher for the Client and Server (out of the box in Ubuntu 20.4 LTS)
- YubiKey with firmware 5.2.3 or higher
```bash
lsusb -v 2>/dev/null | grep -A2 Yubico | grep "bcdDevice"
```

## Setup

### Generate ecdsa-sk key on the client

```bash
ssh-keygen -t ecdsa-sk
Generating public/private ecdsa-sk key pair.
You may need to touch your authenticator to authorize key generation.
Enter PIN for authenticator: [FIDO2-PIN]
Enter file in which to save the key (/home/dev/.ssh/id_ecdsa_sk): 
Enter passphrase (empty for no passphrase): [PASSPHRASE]
Enter same passphrase again: [PASSPHRASE]
Your identification has been saved in /home/dev/.ssh/id_ecdsa_sk
Your public key has been saved in /home/dev/.ssh/id_ecdsa_sk.pub
The key fingerprint is:
SHA256:WXYZ dev@ubuntu
The key's randomart image is:
+-[ECDSA-SK 256]--+
|   ++.=          |
|     * *         |
|  . = =          |
|   = .           |
|                 |
|                 |
|                 |
|                 |
|                 |
+----[SHA256]-----+
```

### Copy the public key to the server

```bash
# Client: Copy the public key
cat /home/dev/.ssh/id_ecdsa_sk.pub

# Server 

```
