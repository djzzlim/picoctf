# [Commitment Issues](https://play.picoctf.org/practice/challenge/411)

## Challenge Information

- **Category**: General Skills
- **Difficulty**: Easy
- **Description**: I accidentally wrote the flag down. Good thing I deleted it!

## Solution Overview

This challenge tests understanding of Git version control concepts, particularly how Git's commit history preserves previous states of files. Even though the flag was "deleted" in the latest commit, we can recover it by checking out a previous commit where it was still present.

## Hints

1. Version control can help you recover files if you change or lose them!
2. Read the chapter on Git from the picoPrimer: https://primer.picoctf.org/#_git_version_control
3. You can 'checkout' commits to see the files inside them

## Detailed Walkthrough

### Step 1: Examining the Repository

First, we download and extract the challenge files, which contain a Git repository. We use `git log` to view the commit history:

```bash
git log
```

Output:
```
commit 3899edb7f3110d613c72ad40083fd8feeef703d0 (HEAD -> master)
Author: picoCTF <ops@picoctf.com>
Date:   Sat Mar 9 21:09:58 2024 +0000
    remove sensitive info
commit 6603cb4ff0c4ea293798c03a32e0d78d5ab12ca2
Author: picoCTF <ops@picoctf.com>
Date:   Sat Mar 9 21:09:58 2024 +0000
    create flag
```

From this log, we can see:
- The latest commit (HEAD) has the message "remove sensitive info"
- A previous commit with ID `6603cb4ff0c4ea293798c03a32e0d78d5ab12ca2` has the message "create flag"

### Step 2: Reverting to the Previous Commit

Since the flag was likely created in the earlier commit and then removed in the latest commit, we checkout the previous commit to access the flag:

```bash
git checkout 6603cb4ff0c4ea293798c03a32e0d78d5ab12ca2
```

Output:
```
Note: switching to '6603cb4ff0c4ea293798c03a32e0d78d5ab12ca2'.
You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.
If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:
  git switch -c <new-branch-name>
Or undo this operation with:
  git switch -
Turn off this advice by setting config variable advice.detachedHead to false
HEAD is now at 6603cb4 create flag
```

### Step 3: Finding the Flag

Now that we've reverted to the state where the flag was created, we can check the repository for the flag file. We find a file named `message.txt`:

```bash
cat message.txt
```

Output:
```
picoCTF{s@n1t1z3_9539be6b}
```

## Flag

```
picoCTF{s@n1t1z3_9539be6b}
```

## Learning Points

- **Git Version Control**: Understanding how Git preserves the history of changes
- **Commit Navigation**: Learning to navigate between different commits to access previous states
- **Data Recovery**: Understanding that "deleted" information may still be accessible in version control systems
- **Digital Forensics**: Basic forensic technique of examining history to recover deleted information

## Mitigation Strategies

To prevent sensitive information from remaining in Git repositories:
- **Git Filter-Branch/BFG**: Tools to permanently remove sensitive data from Git history
- **Pre-commit Hooks**: Implement checks to prevent committing sensitive information
- **GitLeaks**: Use tools to scan repositories for secrets
- **Git Good Practices**: Never commit sensitive information in the first place

## References

- [Git Documentation](https://git-scm.com/doc)
- [picoCTF Git Primer](https://primer.picoctf.org/#_git_version_control)
- [GitHub Docs: Removing sensitive data from a repository](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository)