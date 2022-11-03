# The Salsa Serde Tutorial ! 
## Using the [Serde](https://serde.rs/) library to restructure Rust into JSON.

<br/>
<br/>

![](https://i.imgur.com/UAZlXYm.png)

<br/>
<br/>

___
### Getting Set up
> For this tutorial, we'll be using Visual Studio Code.
> Start by opening your command line and follow along.
* First, you'll need to make sure you have [rust installed](https://www.rust-lang.org/tools/install) on your machine if you don't already.
`curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh`

* Create a new file in your workspace directory named 'Serde'.
`$cargo new Serde`
* Change into your 'Serde' directory 
 `$ cd Serde`
*  Open your IDE
`$ code .`
* In your Cargo.toml file, add the following snippet under **[dependencies]**
```
serde = { version = "1.0", features = ["derive"] }

serde_json = "1.0"
```
* In your Cargo.toml file, add the following snippet under [package]
```
name = "Serde"
version = "0.1.0"
edition = "2021"
```
* Lastly, let's quickly build the project to import our dependencies. 
Open your command line in VSCode [`^`+`~`] and run `cargo build`
___

 ![](https://i.imgur.com/551U3kE.png)
 
---
Serde is an extreamly powerful tool that developers can use to turn Rust code into a wide range of other filing formats. 

This process is known as '**Serialization**', which can support nearly all data types in Rust.

Serde also allows us to '**Deserialize**' files such as JSON data structures into custom formats we program in Rust. 
<br/>
<br/>
# Start Coding

We'll first want to import the nessesary crates into our working directory above the main function.
```
use serde::{Deserialize, Serialize};
use serde_json;
```

Serde has a feature called **derive** which we'll be using in our program to make some tasty salsa. 

`#[derive(Debug, Deserialize, PartialEq, Eq, Serialize)]`

We really only need the Deserialize and Serialize functions, but later in the *recipe*, we'll be using the other features to see if our recipe is correct before and after serialization.
<br/>
<br/>
### Salsa Serde Time!
Above the main function, create a data structure that with the following ingredients. 
```
pub struct Salsa {  
    pub tomatoe: i32, 
    pub lime_juice: String, 
    pub cilantro_leaves: String, 
    pub salt: bool, 
    pub tabasco: bool,
}
```
> **Delicious** ...

Now that we know what ingredients we need to make *Salsa Serde*, we still need to know how much of each ingredient we will need to use. 

In the scope of the main function, create a salsa **Struct** and label how much of each ingredient you will need to make the "best salsa recipe in the world" -- according to the [Washington Grow](https://www.wagrown.com/recipes/speedy-blender-salsa/?gclid=Cj0KCQjwqoibBhDUARIsAH2OpWgnhIP0pynFfnoWVMPgp81ohgWpH04SRuzgBQMjVPCFZC8CIKuKPv8aAndQEALw_wcB).
```
 let salsa = Salsa { 
        tomatoe: 3, 
        lime_juice: "1 TBSP".to_string(), 
        cilantro_leaves: "1/3 Cup".to_string(), 
        salt: true, 
        tabasco: true,
    };
```
<br/>

## It's Serde Blending Time 🔥🔥🔥🔥

![](https://i.imgur.com/i6ekA3p.png)
<br/>
In this tutorial, when I say "blending", it is the analogy for *serialization*. In order to turn a Rust data structure into formatted JSON object, we will use the **Serde** crate to pass in our `Salsa` data structure to convert our recipe from a Rust to a JSON structure.

> **DUMP INGREDIENTS INTO YOUR TOASTMASTER**

To do so, write this line of code bellow your **Salsa Struct**

`let json_str = serde_json::to_string(&salsa).unwrap();`

> **TURN ON THE BLENDER**

Type the following print statement to *serialize* your new Salsa Serde recipe.

`println!("Serialize: {}", json_str);`

> **Explaination** : We declared a new structure named `json_str` to denote that this will turn our salsa `struct` into a JSON object. First we pointed the `serde_json` function at our Salsa data structure, and then we recieved our type string instance after it was successfuly unwrapped it. This will then allow us to print the serialized Rust>JSON Serde Model. 

---
</br>

### Run your code : Part 1 ✨
> It's time to see how our Salsa Serde turned out. 😋

</br>
Open your command line in VS Code [`^`+`~`] and run the following command. 
` $ cargo run`

You should see a return value that looks like this. 
```
Serialize: {"tomatoe":3,"lime_juice":"1 TBSP","cilantro_leaves":"1/3 Cup","salt":true,"tabasco":true}
```

If you do not have any errors, then you have successfully converted a Rust data structure into a JSON object. If you do have errors, go back and make sure you formatted your code within the appropriate scope in the previous directions.

 </br>

---
<br/>

## How to deserialize JSON back into a Rust structure?

> In real life, it wouldn't be possible to turn salsa back into it's original ingredients. However, with Salsa **Serde**, *magical*  things do indeed  happen. ✨ 

In our code editor, bellow our previously created *serialization* structure, write the following line of code to start working your magic. 

`let work_from_json: Salsa = serde_json::from_str(json_str.as_str()).unwrap();`

Once again, we create a new structure named `work_from_json` and orient its inferred type as `Salsa`. 

Our goal is to have **Serde** map the values in our serialized `json_str` from a JSON model to a Rust Struct. In order to make that happen, we tell our `from_str` method to pass the `json_str.as_str()` as its only argument. Lastly, we unwrap the JSON string which will allow us to return a Rust data structure.

> It's time to see some magic happen! 

Type the following print method to see your deserialized salsa recipe transform back into it's original `Salsa` recipe data structure.

`println!("Deserialize: {:?}", work_from_json);`

<br/>

---
<br/>

### Run your code :  Part 2 ✨
`$ cargo run`

> ###### 🪄 Abracadabra - Salsa Serde ! 

You should see the following output in your Terminal.

`Deserialize: Salsa { tomatoe: 3, lime_juice: "1 TBSP", cilantro_leaves: "1/3 Cup", salt: true, tabasco: true }`

<br/>

---

<br/>

### How to format deserialized JSON objects in Rust?

> You have successfully made the worlds best Salsa Serde on earth! The entire family can't stop dipping their chips into your Salsa Serde; and after some time, all of the Salsa is gone! Everyone begins to panic, demanding that you write the secret recipe on a magical stone tablet to share the magic of the Salsa **Serde** ✨ 

<br/>

In order to format a serialized JSON structure correctly, we will need to implement a standard formatting function to display the Salsa Recipe in Rust. 


<br/>

**Above our main function**, write the following code snippet.
```
impl std::fmt::Display for Salsa { 
    fn fmt(&self, f: &mut std::fmt::Formatter<'_>) -> std::fmt::Result { 
        write!(
            f,
            "\n---\nSALSA SERDE:\n tomatoes: {}\n lime_juice: {}\n cilantro_leaves: {}\n salt: {}\n tabasco: {} \n---",
            self.tomatoe, self.lime_juice, self.cilantro_leaves, self.salt, self.tabasco
        )
    }
}
```
Here you can see we've created a new function named `fmt` that expects two arguements which will accept our existing public varibles related to the Serialized Salsa **Struct**, and a **mutable** field of the values that will format our JSON object. We want to return a **formated** string containing the results of our serialized JSON salsa recipe and `write!` it on our *stone tablet* ("Terminal").

<br/>

**Back in our Main function**: 
Go to the bottom of body of the main function and write the same line of of code you did for `work_from_json`, without `{:?}`

```
let work_from_json2: Salsa = serde_json::from_str(json_str.as_str()).unwrap();
    println!("Deserialized V2: {}", work_from_json2);
```
Since we are not debugging our recipe, there is no need for `:?`

<br/>

---

<br/>

### Run your code : Part 3 ✨
`$ cargo run`

<br/>

![](https://i.imgur.com/SngW46h.png)

> By the holy light... The Salsa Serde has finally arrived ! ✨✨✨ Now everyone can happily feast 

<br/>

---

### Final words
I hope this Tutorial was fun for you to go through. **Serde** is a powerful tool with many other features that you should take the time to explore in depth to apply to your own projects. It's the perfect library for formating data you recieve from API's for real time web applications, and for quickly parsing various file types for Web Assembly programs.
