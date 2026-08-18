# Why BIOS Date and Time Need to Be Correct

During Ubuntu installation I had a problem where the installer was stuck on the loading screen.

After checking the logs, I found warnings related to certificates:

```
make-ssl-cert: Could not get FQDN, using '(none)'
```

The problem was caused by an incorrect BIOS date and time.

## Why does the date matter?

Linux uses the system time for many things:

- checking if certificates are valid
- secure connections (SSL/TLS)
- verifying packages
- starting some system services

Certificates have a start and expiration date.

Example:

```
Certificate valid:
01.01.2026 - 01.01.2027
```

If the computer date is wrong:

```
Computer date:
01.01.2010
```

Linux thinks the certificate is not valid yet.

If the date is too far in the future:

```
Computer date:
01.01.2030
```

Linux thinks the certificate is already expired.

Because my BIOS date was incorrect, Ubuntu could not correctly initialize some services during startup.

After fixing the BIOS date and time, the installer started normally.

## What I learned

Before trying complicated fixes, always check basic BIOS settings:

- Date and time
- Boot mode
- Secure Boot
- Storage detection

A small incorrect setting in BIOS can cause problems later during Linux installation.
