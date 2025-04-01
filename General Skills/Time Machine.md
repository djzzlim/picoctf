# [Time Machine](https://play.picoctf.org/practice/challenge/425)

## Challenge Information

- **Category**: General Skills  
- **Difficulty**: Easy  
- **Description**: What was I last working on? I remember writing a note to help me remember...
  You can download the challenge files here:
  - [Challenge Files](https://artifacts.picoctf.net/c_titan/67/challenge.zip)

## Solution Overview

This challenge involves analyzing a Git repository to retrieve a forgotten note. Git stores all changes and commit messages, so by inspecting the commit history, we can recover the flag.

## Hints

1. The `cat` command will let you read a file, but that won't help you here!
2. Read the chapter on Git from the picoPrimer [here](https://primer.picoctf.org/#_git_version_control).
3. When committing a file with git, a message can (and should) be included.

## Detailed Walkthrough

### Step 1: Extracting the Challenge Files

First, we extract the provided challenge ZIP file:

```bash
unzip challenge.zip
cd challenge/drop-in
ls -la
```

The output reveals a `.git` directory, indicating that this is a Git repository:

```bash
total 16
drwxr-xr-x 3 user user 4096 Mar 10  2024 .
drwxr-xr-x 3 user user 4096 Apr  1 20:26 ..
drwxr-xr-x 8 user user 4096 Apr  1 20:26 .git
-rw-r--r-- 1 user user   87 Mar 10  2024 message.txt
```

### Step 2: Checking Git Log

Since commit messages might contain the flag, we check the commit history:

```bash
git log --oneline
```

This outputs:

```bash
b92bdd8 (HEAD -> master) Initial commit: picoCTF{t1m3m@ch1n3_5cde9075}
```

### Step 3: Alternative Approach - Inspecting Git Logs Directly

If the `git` command is unavailable, we can manually check the logs:

```bash
cat .git/logs/refs/heads/master
```

This displays:

```bash
0000000000000000000000000000000000000000 b92bdd8ec87a21ba45e77bd9bed3e4893faafd0f picoCTF 1710018629 +0000 commit (initial): picoCTF{t1m3m@ch1n3_5cde9075}
```

## Flag

```
picoCTF{t1m3m@ch1n3_5cde9075}
```

## Learning Points

- **Git Basics**: Understanding how Git tracks changes and logs commit history.
- **Commit Messages**: Important information is often stored in commit messages.
- **Git Log Navigation**: Using `git log` and `.git` logs to retrieve past activity.

## Mitigation Strategies

To prevent sensitive information exposure in Git repositories:

- **Avoid storing sensitive data in commit messages**.
- **Use `.gitignore` to exclude sensitive files from commits**.
- **Rebase or squash commits if sensitive information is mistakenly committed**.

## References

- [Git Documentation](https://git-scm.com/doc)
- [Using `git log` for Commit History](https://git-scm.com/docs/git-log)

