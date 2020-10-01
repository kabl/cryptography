# Yubico SSH Login

Goal: Using the YubiKey for SSH login as a second factor - 2FA. 

## Setup

Setup a VM (for example on DigitalOcean) where you are able to login with your SSH Key. 

[SSH Key Tutorial](https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys-2)

## Generate API key from yubico

[Yubico API key signup
](https://upgrade.yubico.com/getapikey/)

Copy the `Client ID` and the `Secret key`. 

## Prepare the SSH server

All the following commands have to be executed/configured on the SSH Server.

If you are not working as `root` add the `sudo` command in front of the commands. 

If you want to use an other user than root for the SSH login, replace root with your specific username.

### Add required libraries

```bash
add-apt-repository ppa:yubico/stable
apt-get update
apt-get install libpam-yubico
```

### Update PAM settings

Replace `Client ID` and `Secret key` with the right values. 

```bash
vi /etc/pam.d/sshd

# Add in the first line
auth required pam_yubico.so id=[Client ID] key=[Secret key] debug authfile=/etc/yubikey_mappings mode=client

# Comment this line out. We do not want password login as fallback. 
@include common-auth
```

Get the YubkKey OTP password. To receive the OTP password simple touch the YubiKey while an editor or the terminal is active. It will print out a set of characters. Copy the first twelve characters. 

Create a new File `/etc/yubikey_mappings`

```bash
vi /etc/yubikey_mappings

# Adding the user and the first 12 characters of the  Yubikey OTP
root:[12 first OTP characters]
user1:[...]
```
### Enable authenticate publickey and pam

```bash
vi /etc/ssh/sshd_config

# Enable or add following setting
ChallengeResponseAuthentication yes
AuthenticationMethods publickey,keyboard-interactive:pam
UsePAM yes
```

### Restart sshd

Make sure do not logout of your ssh session. If the configuration is wrong or something failed you might not be able to login with SSH again. 

```bash
service sshd restart
```

## Testing

On the client try to login to the SSH server. 

```bash
# Optional parameter: -v. Verbose option. Helpful for debugging

ssh root@my-server
Enter passphrase for key '/home/user/.ssh/id_rsa': 
YubiKey for `root': 

```
First you should have to enter the password of your ssh keystore file. Afterwards touch the YubiKey. 


## Resources

Original [blog post](https://monicalent.com/blog/2017/12/16/ssh-via-yubikeys-ubuntu/).