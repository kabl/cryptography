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

# Output
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

- Replace [FIDO2-PIN] with the PIN of your FIDO hardware device (e.g. YubiKey)
- Adding an optional [PASSPHRASE] for the SSH certificate (respective to protect the corresponding private key)

It`s strongly recommended to use a PASSPHRASE. Otherwise everybody who has physical access to the hardware device is capable to login.

### Copy the public key to the server

```bash
# Client: Copy the public key
cat /home/dev/.ssh/id_ecdsa_sk.pub

# Server 

```

## DigitalOcean Setup

When creating a Droplet (Ubuntu 20.04 (LTS) x64) in DigitalOcean, it's required to use a "standard" key as SSH key. Such as RSA or ECDSA. DigitaloOcean does not let you enter a `ecdsa-sk` key. 

- Create the droplet and add your standard SSH key in the Authentication section. 

```bash
# Create a temporary standard key
ssh-keygen

# Replace "dev" with your username
cat /home/dev/.ssh/id_rsa.pub
```

- Copy the output to DigitalOcean "New SSH Key". 
- Create the Droplet
- Create the FIDO2 SSH key-pair

```bash
ssh-keygen -t ecdsa-sk
cat /home/dev/.ssh/id_ecdsa_sk.pub
```

- Login to the created VM/Droplet. 
- Replace the keys 

```bash
# Remove the current public key 
echo "" > /root/.ssh/authorized_keys

# Add the new ecdsa-sk key
nano /root/.ssh/authorized_keys
# 1. Remove the 
```

Done and it should work out of the box.

## Resources

Original [Blog post](https://cryptsus.com/blog/how-to-configure-openssh-with-yubikey-security-keys-u2f-otp-authentication-ed25519-sk-ecdsa-sk-on-ubuntu-18.04.html)
