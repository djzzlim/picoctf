# [Binary Search](https://play.picoctf.org/practice/challenge/442)  

## Challenge Information  
- **Category:** General Skills  
- **Difficulty:** Easy  
- **Author:** Jeffery John  

## Solution Overview  
This challenge involves using the **binary search algorithm** to efficiently guess a number between **1 and 1000** within at most **10 attempts**. Binary search is a fundamental technique for searching sorted datasets. The goal is to minimize the number of guesses using a divide-and-conquer approach.  

## Hints  
- Have you ever played hot or cold? Binary search is a bit like that.  
- You have a very limited number of guesses. Try larger jumps between numbers!
- The program will randomly choose a new number each time you connect. You can always try again, but you should start your binary search over from the beginning - try around `500`. Can you think of why?

## Detailed Walkthrough

### Step 1: Connecting via SSH  
To start the challenge, connect to the server using SSH:  
```bash  
ssh -p 54927 ctf-player@atlas.picoctf.net
```
Each connection generates a new random number, requiring a fresh search each time.  

### Step 2: Executing Binary Search  
Binary search follows a **divide-and-conquer** strategy:  
1. Start in the middle of the range (guess **500**).  
2. If the number is **lower**, search in the left half.  
3. If the number is **higher**, search in the right half.  
4. Repeat until the correct number is found.  

Since binary search **halves the search space** in each step, it finds the number in at most **log2(1000) ≈ 10** attempts.  

Upon connecting, the interaction proceeds as follows:  
```text  
Welcome to the Binary Search Game!  
I'm thinking of a number between 1 and 1000.  
Enter your guess: 500  
Lower! Try again.  

Enter your guess: 250  
Lower! Try again.  

Enter your guess: 125  
Higher! Try again.  

Enter your guess: 187  
Higher! Try again.  

Enter your guess: 218  
Congratulations! You guessed the correct number: 218  

Here's your flag: picoCTF{g00d_gu355_1597707f}  
```

## Key Takeaways  
- **Binary search minimizes the number of guesses** by halving the range at each step.  
- **Divide and conquer strategies** are useful in cybersecurity tools.  
- **Logarithmic time complexity (O(log n))** makes binary search highly efficient.  

## Tools & Resources Used  
- **SSH** for connecting to the challenge server.  
- **Binary search algorithm** for efficient number guessing.  
- **Logical deduction** to optimize the search strategy.  

## Flag  
```  
picoCTF{g00d_gu355_1597707f}  
```

## Learning Points  
- How **binary search** optimizes searching in sorted lists.  
- Why **logarithmic complexity** is important in cybersecurity and data analysis.  
- How to apply logical deduction to minimize search steps.  

## References  
- [Binary Search Algorithm Explained](https://www.geeksforgeeks.org/binary-search/)  

