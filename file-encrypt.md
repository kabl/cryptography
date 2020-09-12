# File Encryption

Basically there exist two main principle of encrypt files or directories.

1.  File-system Level Encryption: Encrypt a disk partition or a special (big) file which can be decrypted by the OS and be mounted.
2.  File Encryption: Encrypt each file separately.

By the File-system Level Encryption a change in the decrypted (mounted partition) may affect a big change in the encrypted data. If you want to backup the encrypted data in a cloud service, you've got by every change a big network traffic. By the File Encryption the encrypted data is almost the same size as the content of the decrypted file. This is more useful if you but that data on a cloud service (which you may not trust).

## Setup File Encryption

On Linux you can do File Encryption with Encfs.

```bash
sudo apt-get install encfs
```
Init a base directory. In that directory create two sub-directories.

- crypt: will contain the encrypted data.
- plain: will contain the plain decrypted data

```bash
mkdir crypt plain
```
Create a mount script. Encfs requires absolute paths.
```bash
# mount.sh
CRYPT_DIR=`pwd`/crypt 
PLAIN_DIR=`pwd`/plain 
encfs $CRYPT_DIR $PLAIN_DIR

# Save that script under "mount.sh" and make it executable
chmod u+x mount.sh
```

Run the script. If you run it the first time you will be prompted which option you want to use. I recommend the option "p" for paranoia. After that you have to enter twice the initial password. Use a good one. And don't forget it!

```bash
$ ./mount.sh
```

In the "crypt" directory there should be now a hidden file ".encfs6.xml". If you run the "mount" command you should see an entry which starts with "encfs ...".

## Work with encfs

To mount the encrypted files just run the command mount.sh

```bash
./mount.sh
```

To umount the mounted plain directory you need root rights.

```bash
sudo umount plain
```

If you have mounted the encrypted files you can work in the plain directory as usual. If you're finish with the work just unmount it. Have a look how it looks on the filesystem in a mounted state.