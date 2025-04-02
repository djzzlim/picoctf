# [Super SSH](https://play.picoctf.org/practice/challenge/424)

## Challenge Information

- **Category**: General Skills  
- **Difficulty**: Easy  
- **Description**: Using a Secure Shell (SSH) is going to be pretty important. Can you `ssh` as `ctf-player` to `titan.picoctf.net` at port `62146` to get the flag? You'll also need the password `6dd28e9b`. If asked, accept the fingerprint with `yes`.

## Solution Overview

This challenge introduces the basic usage of SSH (Secure Shell) to connect to remote servers. By correctly using the SSH command with the provided credentials, we can connect to the remote server and retrieve the flag.

## Hints

1. Check the SSH manual page: https://linux.die.net/man/1/ssh
2. You can try logging in 'as' someone with `<user>`@titan.picoctf.net
3. How could you specify the port?
4. Remember, passwords are hidden when typed into the shell

## Detailed Walkthrough

### Step 1: Understanding the SSH Command

SSH (Secure Shell) is a protocol used to securely connect to remote servers. The basic syntax for SSH is:

```bash
ssh [options] [user@]hostname
```

For this challenge, we need to:
- Connect as user `ctf-player`
- To host `titan.picoctf.net`
- On port `62146` (which requires the `-p` option)
- Using password `6dd28e9b`

### Step 2: Establishing the SSH Connection

We execute the SSH command with the appropriate parameters:

```bash
ssh -p 62146 ctf-player@titan.picoctf.net
```

When prompted about the host's fingerprint, we type `yes` to accept it:

```
The authenticity of host '[titan.picoctf.net]:62146 ([3.139.174.234]:62146)' can't be established.
ED25519 key fingerprint is SHA256:4S9EbTSSRZm32I+cdM5TyzthpQryv5kudRP9PIKT7XQ.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
```

### Step 3: Entering the Password

When prompted for a password, we enter `6dd28e9b`. Note that for security reasons, the password characters are not displayed as you type:

```
ctf-player@titan.picoctf.net's password: 
```

### Step 4: Retrieving the Flag

After successful authentication, we are automatically presented with the flag:

```
Welcome ctf-player, here's your flag: picoCTF{s3cur3_c0nn3ct10n_5d09a462}
Connection to titan.picoctf.net closed.
```

## Flag

```
picoCTF{s3cur3_c0nn3ct10n_5d09a462}
```

## Learning Points

- **SSH Basics**: Understanding how to use SSH to connect to remote servers
- **Command-line Options**: Using the `-p` flag to specify a non-standard port
- **Authentication Methods**: Using username/password authentication
- **Host Key Verification**: Understanding the importance of verifying host keys for security

## Mitigation Strategies

Best practices for secure SSH use include:

- **Use Key-Based Authentication** instead of passwords when possible
- **Limit SSH Access** to specific users and IP addresses
- **Change Default Ports** to reduce automated attacks
- **Keep SSH Software Updated** to patch security vulnerabilities

## References

- [SSH Command Documentation](https://linux.die.net/man/1/ssh)
- [PicoCTF Primer on The Shell](https://primer.picoctf.com/#_the_shell)