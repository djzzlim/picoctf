# [Rust fixme 3](https://play.picoctf.org/practice/challenge/463)

## Challenge Information

- **Category**: General Skills
- **Difficulty**: Easy
- **Description**: Have you heard of Rust? Fix the syntax errors in this Rust file to print the flag! Download the Rust code [here](https://challenge-files.picoctf.net/c_verbal_sleep/dcdaf491b35c1d0f5075e9583edbbb7aaea1dffb6ad32bc000e4d87b5200ff7b/fixme3.tar.gz).

## Solution Overview

This challenge involves debugging a Rust program with syntax errors. The goal is to fix these errors so the program can successfully compile and reveal the flag.

## Hints

- **Read the comments...darn it!**

## Detailed Walkthrough

### Step 1: Understanding the Rust Code

We are provided with the following Rust source file:

```rust
use xor_cryptor::XORCryptor;

fn decrypt(encrypted_buffer: Vec<u8>, borrowed_string: &mut String) {
    // Key for decryption
    let key = String::from("CSUCKS");

    // Editing our borrowed value
    borrowed_string.push_str("PARTY FOUL! Here is your flag: ");

    // Create decryption object
    let res = XORCryptor::new(&key);
    if res.is_err() {
        return;
    }
    let xrc = res.unwrap();

    // Did you know you have to do "unsafe operations in Rust?
    // https://doc.rust-lang.org/book/ch19-01-unsafe-rust.html
    // Even though we have these memory safe languages, sometimes we need to do things outside of the rules
    // This is where unsafe rust comes in, something that is important to know about in order to keep things in perspective
    
    // unsafe {
        // Decrypt the flag operations 
        let decrypted_buffer = xrc.decrypt_vec(encrypted_buffer);

        // Creating a pointer 
        let decrypted_ptr = decrypted_buffer.as_ptr();
        let decrypted_len = decrypted_buffer.len();
        
        // Unsafe operation: calling an unsafe function that dereferences a raw pointer
        let decrypted_slice = std::slice::from_raw_parts(decrypted_ptr, decrypted_len);

        borrowed_string.push_str(&String::from_utf8_lossy(decrypted_slice));
    // }
    println!("{}", borrowed_string);
}

fn main() {
    // Encrypted flag values
    let hex_values = ["41", "30", "20", "63", "4a", "45", "54", "76", "12", "90", "7e", "53", "63", "e1", "01", "35", "7e", "59", "60", "f6", "03", "86", "7f", "56", "41", "29", "30", "6f", "08", "c3", "61", "f9", "35"];

    // Convert the hexadecimal strings to bytes and collect them into a vector
    let encrypted_buffer: Vec<u8> = hex_values.iter()
        .map(|&hex| u8::from_str_radix(hex, 16).unwrap())
        .collect();

    let mut party_foul = String::from("Using memory unsafe languages is a: ");
    decrypt(encrypted_buffer, &mut party_foul);
}
```

### Step 2: Identifying Syntax Errors

The provided code contains multiple syntax issues:

1. **Missing `unsafe` block:**
    
   The function `std::slice::from_raw_parts` dereferences a raw pointer, which is unsafe in Rust. Rust enforces memory safety by requiring `unsafe` blocks for such operations.
   
   ```rust
   unsafe {
       let decrypted_slice = std::slice::from_raw_parts(decrypted_ptr, decrypted_len);
   }
   ```
   
2. **Missing `unsafe` around pointer dereferencing**:
   
   The lines where `decrypted_ptr` and `decrypted_len` are used in `from_raw_parts` require an `unsafe` block because raw pointers can lead to undefined behavior if misused.
   
3. **Code should be modified to correctly include the `unsafe` block.**

### Step 3: Fixing the Rust Code

Here is the corrected version of the Rust program:

```rust
use xor_cryptor::XORCryptor;

fn decrypt(encrypted_buffer: Vec<u8>, borrowed_string: &mut String) {
    // Key for decryption
    let key = String::from("CSUCKS");

    // Editing our borrowed value
    borrowed_string.push_str("PARTY FOUL! Here is your flag: ");

    // Create decryption object
    let res = XORCryptor::new(&key);
    if res.is_err() {
        return;
    }
    let xrc = res.unwrap();

    // Did you know you have to do "unsafe operations in Rust?
    // https://doc.rust-lang.org/book/ch19-01-unsafe-rust.html
    // Even though we have these memory safe languages, sometimes we need to do things outside of the rules
    // This is where unsafe rust comes in, something that is important to know about in order to keep things in perspective
    
    unsafe {
        // Decrypt the flag operations 
        let decrypted_buffer = xrc.decrypt_vec(encrypted_buffer);

        // Creating a pointer 
        let decrypted_ptr = decrypted_buffer.as_ptr();
        let decrypted_len = decrypted_buffer.len();
        
        // Unsafe operation: calling an unsafe function that dereferences a raw pointer
        let decrypted_slice = std::slice::from_raw_parts(decrypted_ptr, decrypted_len);

        borrowed_string.push_str(&String::from_utf8_lossy(decrypted_slice));
    }
    println!("{}", borrowed_string);
}

fn main() {
    // Encrypted flag values
    let hex_values = ["41", "30", "20", "63", "4a", "45", "54", "76", "12", "90", "7e", "53", "63", "e1", "01", "35", "7e", "59", "60", "f6", "03", "86", "7f", "56", "41", "29", "30", "6f", "08", "c3", "61", "f9", "35"];

    // Convert the hexadecimal strings to bytes and collect them into a vector
    let encrypted_buffer: Vec<u8> = hex_values.iter()
        .map(|&hex| u8::from_str_radix(hex, 16).unwrap())
        .collect();

    let mut party_foul = String::from("Using memory unsafe languages is a: ");
    decrypt(encrypted_buffer, &mut party_foul);
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
picoCTF{n0w_y0uv3_f1x3d_1h3m_411}
```

## Tools and Resources Used

- **Rust Compiler (`rustc`)**: For compiling Rust code.
- **Cargo**: Rust’s package manager.
- **XORCryptor Crate**: Used for XOR decryption.
- **Rust documentation**: To understand `unsafe` operations.

## Flag

```
picoCTF{n0w_y0uv3_f1x3d_1h3m_411}
```

## Learning Points

- **Understanding `unsafe` blocks in Rust.**
- **Proper handling of raw pointers and memory safety in Rust.**
- **How to debug Rust compiler errors related to unsafe operations.**

## Mitigation Strategies

To avoid similar syntax errors when writing Rust programs:

- **Read Rust compiler error messages carefully.**
- **Use `unsafe` only when absolutely necessary.**
- **Refer to Rust’s official documentation for memory safety guidelines.**

## References

- [Unsafe Rust](https://doc.rust-lang.org/book/ch19-01-unsafe-rust.html)
- [Rust Error Handling](https://doc.rust-lang.org/rust-by-example/error.html)

