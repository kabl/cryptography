# GPG Notes

## Init

```bash
# Generate key
gpg --generate-key
# List private / public keys
gpg --list-secret-keys
gpg  --list-public-keys

# Create a file with content
echo "hello" > text.txt
```

## Signatures

```bash
# Sign data. Generates an envelope with the data and the signature
gpg --sign text.txt
> text.txt.gpg

# Verify the signature
gpg --verify text.txt.gpg

# Create a detached signature
gpg --detach-sign text.txt
> text.txt.sig

# Verify the signature
gpg --verify text.txt.sig text.txt
```

## Encryption
```bash
# Encrypt symmetric
gpg --symmetric text.txt
> text.txt.gpg

# Decrypt
gpg --decrypt text.txt.gpg

# Encrypt asymmetric. User ID recipient required
gpg --encrypt text.txt
> text.txt.gpg

# Decrypt
gpg --decrypt text.txt.gpg

## Encrypt and Sign
gpg --encrypt --sign text.txt
> text.txt.gpg
```

## Key Management
```bash
gpg --export -a "User Name" > public.key
gpg --import public.key
```

## Base64
Used to transfer data from bin to ASCII and vis-versa
```bash
# Encode data to ASCII
base64 data.bin > data.bin.b64

# Decode ASCII to original content
base64 --decode data.bin.b64 > data.bin
```