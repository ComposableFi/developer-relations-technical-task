# The Salsa Serde Tutorial ! 
## Familiarizing ourselves with the [Serde](https://serde.rs/) Library
<br/>


![](https://i.imgur.com/UAZlXYm.png)

<br/>
<br/>
<br/>
<br/>

___
### Getting Set up
> For this Tutorial, we'll be using Visual Studio Code.
> Start by opening your command line and follow along.
* First, you'll need to make sure you have [rust installed](https://www.rust-lang.org/tools/install) on your machine if you don't already.
`curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh`

* Create a new file in your workspace directory named 'Serde'.
`$cargo new Serde`
* Change into your 'Serde' directory 
 `$ cd Serde`
*  Open your IDE
`$ code .`
* In your Cargo.toml file, add the following snippet under [dependencies]
```
serde = { version = "1.0", features = ["derive"] }

serde_json = "1.0"
```
* in your Cargo.toml file, add the following snippet under [package]
```
name = "Serde"
version = "0.1.0"
edition = "2021"
```
* Lastly, let's quickly build the project. 
Open your Command line ins VSCode [`^`+`~`] and enter `cargo build`
___

## What is Serde? 



