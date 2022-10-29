In this task, we'll write a fully fletched tutorial about a library that you probably are unfamiliar with but is used everywhere in the Rust ecosystem: [serde](https://serde.rs/).

Your goals for the tutorial are:

1. Use a lively example to illustrate what Serde can do.
2. Go through the main features, and show some more obscure ones.
3. Make it enjoyable. We do not want to see the same structure as the official docs.

For this task, create a pull request with a single file, `tutorial.md`, which contains your tutorial. Code examples should be included as code blocks.

Most likely you'll be writing a bit of Rust here. You are free to plagiarize existing examples from the internet, but the following should hold:

- It compiles.
- Clippy doesn't emit warnings.
- It is pleasant yet straightforward to read.

For your Rust code, you can use the [playground](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021&gist=4dc7dcf61540a5c39af540edf18b361a). It contains all the code, and can even be embedded. We've already created a brief example, but serde has many more features.

## How will we evaluate the task?

- Does the tutorial cover the main features of Serde, and does it add value over existing tutorials?
- Is the tutorial interesting to read?
- Is the code of high quality?

For the last part, you are free to call on friends, StackOverflow, or other resources. 

Use spelling checkers, Grammarly, and linters to ensure that your tutorial is of high quality.

## Ideas for the tutorial

- Reading the Coinbase API using Rust.
- Alternative Cosmwasm serialization for higher performance (difficult).
- Using Serde to serialize and deserialize a custom data structure, with advanced types (difficult).
- Whatever else you can think of!

## Intended Audience

- Junior developers should find this challenging, and possibly the reason to go into Rust development.
- Intermediate developers should already be familiar with the content.

## Resources

Some blogs/books that we find fantastic:

- [fasterthanli](https://fasterthanli.me)
- [zero2prod.com](https://www.zero2prod.com/)