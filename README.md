# Number Guessing Game (Rust)

This is a simple interactive number guessing game implemented in Rust.  
The game selects a random integer between **1 and 100**, and the player repeatedly enters guesses until they find the correct number. After each input, the program indicates whether the guess is **too small**, **too big**, or **correct**.

This project demonstrates core language concepts while producing a fun, working console application.

---

## Features Demonstrated

This program exercises several foundational Rust concepts:

### **1. Standard Input Handling**
- Uses `std::io` to read user input.
- Demonstrates building and reusing a mutable `String` buffer.
- Illustrates basic error handling with `.expect`.

### **2. Random Number Generation**
- Uses the `rand` crate for generating a random integer.
- Demonstrates calling `rand::rng().random_range(...)`.

### **3. Variable Shadowing**
- The `guess` string is shadowed as a parsed `u32`.

### **4. Pattern Matching**
- Uses a `match` statement to compare guesses to the secret number using `Ordering`.

### **5. Loops and Control Flow**
- Infinite loop (`loop`) continues until the user guesses correctly.
- `break` exits the loop when the win condition is met.

### **6. Error Handling via `match`**
- Parsing user input into an integer handles invalid input gracefully by continuing the loop.

---

## Source Code

```rust
use std::cmp::Ordering;
use std::io;

use rand::Rng;

fn main() {
    println!("Guess the number!");

    let secret_number = rand::rng().random_range(1..=100);

    loop {
        println!("Please input your guess.");

        let mut guess = String::new();

        io::stdin()
            .read_line(&mut guess)
            .expect("Failed to read line");

        let guess: u32 = match guess.trim().parse() {
            Ok(num) => num,
            Err(_) => continue,
        };

        println!("You guessed: {guess}");

        match guess.cmp(&secret_number) {
            Ordering::Less => println!("Too small!"),
            Ordering::Greater => println!("Too big!"),
            Ordering::Equal => {
                println!("You win!");
                break;
            }
        }
    }
}
```

---

## Prerequisites

You must have the Rust toolchain installed.

Install via Rustup:

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

Check installation:

```bash
rustc --version
cargo --version
```

---

## Building the Game

Inside the project directory:

```bash
cargo build
```

This compiles the game and downloads dependencies such as the `rand` crate.

---

## Running the Game

Run directly with Cargo:

```bash
cargo run
```

You will see:

```
Guess the number!
Please input your guess.
```

Enter a number and press Enter.  
The game will tell you whether your guess is too high, too low, or correct.

---

## Example Session

```
Guess the number!
Please input your guess.
50
You guessed: 50
Too small!
Please input your guess.
75
You guessed: 75
Too big!
Please input your guess.
62
You guessed: 62
You win!
```

---

## Next Steps / Suggested Enhancements

- Add difficulty modes with different number ranges.
- Track the number of guesses and print a score.
- Add error messages for invalid inputs.
- Prevent repeated guesses or offer hints.
- Implement a replay loop.
