# Split and Combine Secrets

Using Shamir's Secret Sharing Scheme.

```bash
# Split a secret. 2 of 4 splits required to recover
ssss-split -t 2 -n 4 -w password
> password-1-3f6eadb4c6c4a0c8f7ad69
> password-2-f9e02dd0c486cbbf2a264a
> password-3-4465adf33ab8ed6d9ea0ea
> password-4-74fd2d18c0021d509130d7

# Recover
ssss-combine -t 2
```