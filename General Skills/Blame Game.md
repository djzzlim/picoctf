# [Blame Game](https://play.picoctf.org/practice/challenge/405)

## Challenge Information

- **Category**: General Skills
- **Difficulty**: Easy
- **Description**: Someone's commits seems to be preventing the program from working. Who is it?

## Solution Overview

This challenge tests understanding of Git commit history and blame tracking. By examining the Git logs, we need to identify which user made commits that might be causing issues with the program.

## Hints

1. In collaborative projects, many users can make many changes. How can you see the changes within one file?
2. Read the chapter on Git from the picoPrimer.
3. You can use `python3 <file>.py` to try running the code, though you won't need to for this challenge.

## Detailed Walkthrough

### Step 1: Downloading and Exploring the Repository

First, we download and extract the challenge files, which contain a Git repository.

### Step 2: Examining the Git Log

To find out who might be causing the issues, we can check the Git logs. One way to do this is to look at the HEAD file in the `.git/logs` directory:

```bash
cat .git/logs/HEAD
```

Output:
```
0000000000000000000000000000000000000000 caa945839a2fc0fb52584b559b4e89ac7c46bf54 picoCTF <ops@picoctf.com> 1710202031 +0000    commit (initial): create top secret project
caa945839a2fc0fb52584b559b4e89ac7c46bf54 8c83358c32daee3f8b597d2b853c1d1966b23f0a picoCTF{@sk_th3_1nt3rn_2c6bf174} <ops@picoctf.com> 1710202031 +0000   commit: optimize file size of prod code
8c83358c32daee3f8b597d2b853c1d1966b23f0a 6f9f8fc8907eefb90424f81d659f717c5c0b2c8a picoCTF <ops@picoctf.com> 1710202031 +0000    commit: important business work
6f9f8fc8907eefb90424f81d659f717c5c0b2c8a 7200e12a5a9cd847e725e883a0a2e228bf965ac0 picoCTF <ops@picoctf.com> 1710202031 +0000    commit: important business work
7200e12a5a9cd847e725e883a0a2e228bf965ac0 c44b476d9c65b973a56d84902039e0a2725cf5b1 picoCTF <ops@picoctf.com> 1710202031 +0000    commit: important business work
c44b476d9c65b973a56d84902039e0a2725cf5b1 ad09e34e0ecaec5fa39c151b6371f69421b6066f picoCTF <ops@picoctf.com> 1710202031 +0000    commit: important business work
...
```

### Step 3: Alternative Method
We can also use `git blame` to see who last modified each line of the file. In this case, let's run:
```bash
git blame message.py
```

Output:
```bash
8c83358c (picoCTF{@sk_th3_1nt3rn_2c6bf174} 2024-03-12 00:07:11 +0000 1) print("Hello, World!"
```

### Step 4: Identifying the Culprit

Looking at the Git log, we notice something unusual. In the second commit, the committer's name is not "picoCTF" but rather "picoCTF{@sk_th3_1nt3rn_2c6bf174}". This stands out from all other commits where the committer is simply "picoCTF".

The unusual committer name contains what appears to be a flag in the standard picoCTF format. This suggests that this is the person whose commits are causing the issues mentioned in the challenge description.

## Flag

```
picoCTF{@sk_th3_1nt3rn_2c6bf174}
```

## Learning Points

- **Git Commit History**: Understanding how to examine commit logs in Git
- **Git Blame**: Learning how to identify who made specific changes in a repository
- **Git Metadata**: Recognizing that Git stores metadata about commits, including author information
- **Forensic Analysis**: Basic forensic technique of examining logs to identify anomalies
- **Collaborative Development**: Understanding challenges in multi-developer environments

## Mitigation Strategies

In real-world development:
- **Code Reviews**: Implement peer review processes to catch problematic commits early
- **Continuous Integration**: Set up automated testing to identify breaking changes
- **Git Hooks**: Use pre-commit hooks to enforce coding standards
- **Proper Attribution**: Ensure all developers use proper identification in Git configuration

## References

- [Git Log Command Documentation](https://git-scm.com/docs/git-log)
- [Git Blame Command Documentation](https://git-scm.com/docs/git-blame)
- [picoCTF Git Primer](https://primer.picoctf.org/#_git_version_control)