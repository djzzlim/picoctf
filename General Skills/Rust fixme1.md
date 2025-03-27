# [Rust fixme 1](https://play.picoctf.org/practice/challenge/XXX)

## Challenge Information

- **Category**: General Skills
- **Difficulty**: Easy
- **Description**: Have you heard of Rust? Fix the syntax errors in this Rust file to print the flag! Download the Rust code [here](https://challenge-files.picoctf.net/c_verbal_sleep/3f0e13f541928f420d9c8c96b06d4dbf7b2fa18b15adbd457108e8c80a1f5883/fixme1.tar.gz).

## Solution Overview

This challenge involves debugging a Rust program with syntax errors. The goal is to fix these errors so the program can successfully compile and reveal the flag.

## Hints

- **Cargo is Rust's package manager and will make your life easier.**
- **Rust has some pretty great compiler error messages. Read them maybe?**
- **Check how Rust functions, variables, and statements are properly formatted.**

## Detailed Walkthrough

### Step 1: Understanding the Rust Code

We are provided with the following Rust source file:

```rust
use xor_cryptor::XORCryptor;

fn main() {
    // Key for decryption
    let key = String::from("CSUCKS") // How do we end statements in Rust?

    // Encrypted flag values
    let hex_values = ["41", "30", "20", "63", "4a", "45", "54", "76", "01", "1c", "7e", "59", "63", "e1", "61", "25", "7f", "5a", "60", "50", "11", "38", "1f", "3a", "60", "e9", "62", "20", "0c", "e6", "50", "d3", "35"];

    // Convert the hexadecimal strings to bytes and collect them into a vector
    let encrypted_buffer: Vec<u8> = hex_values.iter()
        .map(|&hex| u8::from_str_radix(hex, 16).unwrap())
        .collect();

    // Create decryption object
    let res = XORCryptor::new(&key);
    if res.is_err() {
        ret; // How do we return in Rust?
    }
    let xrc = res.unwrap();

    // Decrypt flag and print it out
    let decrypted_buffer = xrc.decrypt_vec(encrypted_buffer);
    println!(
        ":?", // How do we print out a variable in the println function?
        String::from_utf8_lossy(&decrypted_buffer)
    );
}
```

### Step 2: Identifying Syntax Errors

The provided code contains multiple syntax issues:

1. **Missing semicolon (`;`)** after `let key = String::from("CSUCKS")`.
    ```rust
    let key = String::from("CSUCKS");
    ```
2. **Incorrect function call (`ret;`)**; Rust does not have `ret` like C.
    ```rust
    return;
    ```
3. **Incorrect `println!` syntax**; the format string must be specified correctly.
    ```rust
    println!("{}", String::from_utf8_lossy(&decrypted_buffer));
    ```

### Step 3: Fixing the Rust Code

Here is the corrected version of the Rust program:

```rust
use xor_cryptor::XORCryptor;

fn main() {
    // Key for decryption
    let key = String::from("CSUCKS"); // How do we end statements in Rust?

    // Encrypted flag values
    let hex_values = ["41", "30", "20", "63", "4a", "45", "54", "76", "01", "1c", "7e", "59", "63", "e1", "61", "25", "7f", "5a", "60", "50", "11", "38", "1f", "3a", "60", "e9", "62", "20", "0c", "e6", "50", "d3", "35"];

    // Convert the hexadecimal strings to bytes and collect them into a vector
    let encrypted_buffer: Vec<u8> = hex_values.iter()
        .map(|&hex| u8::from_str_radix(hex, 16).unwrap())
        .collect();

    // Create decrpytion object
    let res = XORCryptor::new(&key);
    if res.is_err() {
        return; // How do we return in rust?
    }
    let xrc = res.unwrap();

    // Decrypt flag and print it out
    let decrypted_buffer = xrc.decrypt_vec(encrypted_buffer);
    println!(
        "{}", // How do we print out a variable in the println function? 
        String::from_utf8_lossy(&decrypted_buffer)
    );
}
```

### Step 4: Running the Fixed Code

To compile and run the fixed Rust program, use the following commands:

```bash
cargo build
cargo run
```

### Step 5: Retrieving the Flag

After running the program, we obtain:

```
picoCTF{4r3_y0u_4_ru$t4c30n_n0w?}
```

## Tools and Resources Used

- **Rust Compiler (`rustc`)**: For compiling Rust code.
- **Cargo**: Rust’s package manager.
- **XORCryptor Crate**: Used for XOR decryption.
- **Rust documentation**: To understand proper syntax and error handling.

## Flag

```
picoCTF{4r3_y0u_4_ru$t4c30n_n0w?}
```

## Learning Points

- **Understanding Rust syntax and statement termination.**
- **Proper function return statements in Rust.**
- **Using `println!` correctly with format strings.**
- **How to debug Rust compiler errors.**

## Mitigation Strategies

To avoid similar syntax errors when writing Rust programs:

- **Read Rust compiler error messages carefully.**
- **Use Cargo for dependency management and compilation.**
- **Refer to Rust’s official documentation for proper syntax.**

## References

- [Rust Official Documentation](https://doc.rust-lang.org/book/)
- [Cargo - Rust’s Package Manager](https://doc.rust-lang.org/cargo/)
- [Rust Error Handling](https://doc.rust-lang.org/rust-by-example/error.html)
- [Rust Formatted Print](https://doc.rust-lang.org/rust-by-example/hello/print.html)
