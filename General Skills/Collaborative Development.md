# [Collaborative Development](https://play.picoctf.org/practice/challenge/295967)

## Challenge Information

- **Category**: General Skills
- **Difficulty**: Easy
- **Description**: My team has been working very hard on new features for our flag printing program! I wonder how they'll work together?

## Solution Overview

This challenge tests understanding of Git branching and merging concepts. The flag is split across three different feature branches, and we need to examine each branch's implementation to collect all parts of the flag.

## Hints

1. `git branch -a` will let you see available branches
2. How can file 'diffs' be brought to the main branch? Don't forget to `git config`!
3. Merge conflicts can be tricky! Try a text editor like nano, emacs, or vim.

## Detailed Walkthrough

### Step 1: Examining Available Branches

After downloading and extracting the challenge files, we use `git branch -a` to list all available branches:

```bash
git branch -a
  feature/part-1
  feature/part-2
  feature/part-3
* main
```

We can see that there are three feature branches besides the main branch: `feature/part-1`, `feature/part-2`, and `feature/part-3`.

### Step 2: Exploring the Feature Branches

We need to switch to each feature branch and run the flag printing program to see what each branch outputs.

#### Branch: feature/part-1

```bash
git switch feature/part-1
python flag.py
```

Output:
```
Printing the flag...
picoCTF{t3@mw0rk_
```

This branch provides the first part of the flag.

#### Branch: feature/part-2

```bash
git switch feature/part-2
python flag.py
```

Output:
```
Printing the flag...
m@k3s_th3_dr3@m_
```

This branch provides the middle part of the flag.

#### Branch: feature/part-3

```bash
git switch feature/part-3
python flag.py
```

Output:
```
Printing the flag...
w0rk_7ae8dd33}
```

This branch provides the last part of the flag.

### Step 3: Assembling the Complete Flag

By combining the outputs from all three branches, we get the complete flag:

```
picoCTF{t3@mw0rk_m@k3s_th3_dr3@m_w0rk_7ae8dd33}
```

## Flag

```
picoCTF{t3@mw0rk_m@k3s_th3_dr3@m_w0rk_7ae8dd33}
```

## Learning Points

- **Git Branch Management**: Understanding how to navigate between different branches in a Git repository
- **Collaborative Development**: Seeing how different teams can work on separate features in parallel
- **Code Integration**: Learning about the challenges of integrating code from multiple sources
- **Flag Segmentation**: Recognizing that security flags or sensitive information might be split across different locations

## Mitigation Strategies

In real-world development:
- **Proper Branch Strategy**: Implement a clear branching strategy for collaborative development
- **Code Reviews**: Require peer reviews before merging branches to maintain code quality
- **Automated Testing**: Ensure all branches pass tests before integration
- **Secret Management**: Avoid storing sensitive information like flags or credentials in code repositories

## References

- [Git Branching](https://git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell)
- [Git Branch Command Documentation](https://git-scm.com/docs/git-branch)
- [Git Switch Command Documentation](https://git-scm.com/docs/git-switch)