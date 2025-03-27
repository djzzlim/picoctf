# [Rust Fixme 2](https://play.picoctf.org/practice/challenge/XXX)

## Challenge Information

- **Category**: General Skills
- **Difficulty**: Easy
- **Description**: The Rust saga continues? I ask you, can I borrow that, pleeeeeaaaasseeeee?
Download the Rust code [here](https://challenge-files.picoctf.net/c_verbal_sleep/babfbee79718a6363826ba86300173ffde6d81577e9dd07d4130c53a7eecf6c3/fixme2.tar.gz).

## Solution Overview

The given Rust program has issues related to borrowing and mutability, preventing it from compiling. Our task is to identify and resolve these issues so that the program can properly execute.

## Hints

- **[https://doc.rust-lang.org/book/ch04-02-references-and-borrowing.html](https://doc.rust-lang.org/book/ch04-02-references-and-borrowing.html)**

## Detailed Walkthrough

### Step 1: Understanding the Rust Code

The provided Rust source file contains borrowing errors:

```rust
use xor_cryptor::XORCryptor;

fn decrypt(encrypted_buffer:Vec<u8>, borrowed_string: &String){ // How do we pass values to a function that we want to change?

    // Key for decryption
    let key = String::from("CSUCKS");

    // Editing our borrowed value
    borrowed_string.push_str("PARTY FOUL! Here is your flag: ");

    // Create decrpytion object
    let res = XORCryptor::new(&key);
    if res.is_err() {
        return; // How do we return in rust?
    }
    let xrc = res.unwrap();

    // Decrypt flag and print it out
    let decrypted_buffer = xrc.decrypt_vec(encrypted_buffer);
    borrowed_string.push_str(&String::from_utf8_lossy(&decrypted_buffer));
    println!("{}", borrowed_string);
}


fn main() {
    // Encrypted flag values
    let hex_values = ["41", "30", "20", "63", "4a", "45", "54", "76", "01", "1c", "7e", "59", "63", "e1", "61", "25", "0d", "c4", "60", "f2", "12", "a0", "18", "03", "51", "03", "36", "05", "0e", "f9", "42", "5b"];

    // Convert the hexadecimal strings to bytes and collect them into a vector
    let encrypted_buffer: Vec<u8> = hex_values.iter()
        .map(|&hex| u8::from_str_radix(hex, 16).unwrap())
        .collect();

    let party_foul = String::from("Using memory unsafe languages is a: "); // Is this variable changeable?
    decrypt(encrypted_buffer, &party_foul); // Is this the correct way to pass a value to a function so that it can be changed?
}
```

### Step 2: Identifying Errors

1. **`borrowed_string` is immutable** – attempting to modify it with `.push_str()` will fail.
2. **Incorrect function signature** – should use `&mut String` instead of `&String`.
3. **Attempting to pass an immutable variable** – `party_foul` must be mutable.

### Step 3: Fixing the Rust Code

Correcting the code involves:

1. Changing `borrowed_string: &String` to `borrowed_string: &mut String`.
    ```rust
    fn decrypt(encrypted_buffer:Vec<u8>, borrowed_string: &mut String)
    ```
2. Declaring `party_foul` as `mut`.
    ```rust
    let mut party_foul = String::from("Using memory unsafe languages is a: ");
    ```
3. Passing `&mut party_foul` to `decrypt()`.
    ```rust
    decrypt(encrypted_buffer, &mut party_foul);
    ```

#### Fixed Code:

```rust
use xor_cryptor::XORCryptor;

fn decrypt(encrypted_buffer:Vec<u8>, borrowed_string: &mut String){ // How do we pass values to a function that we want to change?

    // Key for decryption
    let key = String::from("CSUCKS");

    // Editing our borrowed value
    borrowed_string.push_str("PARTY FOUL! Here is your flag: ");

    // Create decrpytion object
    let res = XORCryptor::new(&key);
    if res.is_err() {
        return; // How do we return in rust?
    }
    let xrc = res.unwrap();

    // Decrypt flag and print it out
    let decrypted_buffer = xrc.decrypt_vec(encrypted_buffer);
    borrowed_string.push_str(&String::from_utf8_lossy(&decrypted_buffer));
    println!("{}", borrowed_string);
}


fn main() {
    // Encrypted flag values
    let hex_values = ["41", "30", "20", "63", "4a", "45", "54", "76", "01", "1c", "7e", "59", "63", "e1", "61", "25", "0d", "c4", "60", "f2", "12", "a0", "18", "03", "51", "03", "36", "05", "0e", "f9", "42", "5b"];

    // Convert the hexadecimal strings to bytes and collect them into a vector
    let encrypted_buffer: Vec<u8> = hex_values.iter()
        .map(|&hex| u8::from_str_radix(hex, 16).unwrap())
        .collect();

    let mut party_foul = String::from("Using memory unsafe languages is a: "); // Is this variable changeable?
    decrypt(encrypted_buffer, &mut party_foul); // Is this the correct way to pass a value to a function so that it can be changed?
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
picoCTF{4r3_y0u_h4v1n5_fun_y31?}
```

## Tools and Resources Used

- **Rust Compiler (`rustc`)**: For compiling Rust code.
- **Cargo**: Rust’s package manager.
- **XORCryptor Crate**: Used for XOR decryption.
- **Rust documentation**: To understand ownership, borrowing, and mutability.

## Flag

```
picoCTF{4r3_y0u_h4v1n5_fun_y31?}
```

## Learning Points

- **Understanding Rust’s ownership and borrowing model.**
- **Modifying mutable references properly.**
- **Reading Rust compiler error messages to debug effectively.**

## Mitigation Strategies

To avoid similar borrowing issues in Rust:

- **Understand when to use `&mut` instead of `&`.**
- **Always handle errors safely instead of using `.unwrap()`.**
- **Use Rust's borrow checker to guide safe memory management.**

## References

- [Rust Borrowing and References](https://doc.rust-lang.org/book/ch04-02-references-and-borrowing.html)
- [Rust Error Handling](https://doc.rust-lang.org/rust-by-example/error.html)