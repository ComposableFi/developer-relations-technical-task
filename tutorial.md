# The Salsa Serde Tutorial ! 
## Familiarizing ourselves with the [Serde](https://serde.rs/) Library
<br/>


![](https://i.imgur.com/UAZlXYm.png)

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

 ![](https://i.imgur.com/551U3kE.png)
 
---
Serde is an extreamly powerful tool that developers can use to turn Rust code into a wide range of other filing formats. 

This Process is known as '**Serialization**'. 

We can also '**Deserialize**' a JSON string into a data structure in Rust. 
<br/>

## Start Coding

We'll first want to import the nessesary crates into our working directory. 
```
use serde::{Deserialize, Serialize};
use serde_json;
```

Serde has a feature called **derive** which we'll be using for our crate to make some tasty salsa. 

`#[derive(Debug, Deserialize, PartialEq, Eq, Serialize)]`

We really only need the Deserialize and Serialize functions, but later in the *recipe*, we'll be using the other features to see if our recipe is correct before and after serialization.

### Salsa Serde Time!
create a data structure that with the following ingredients. 
```
pub struct Salsa {  
    pub tomatoe: i32, 
    pub lime_juice: String, 
    pub cilantro_leaves: String, 
    pub salt: bool, 
    pub tabasco: bool,
}
```
Fantastic! 
Now that we kniw what ingredients we need to make Salsa Serde, we need to know how much of each ingredient we need. 

In your main function, create a salsa **Struct** and lable how much of each ingredient you will need to make the best salsa recipe in the world -- according to the [washington grow](https://www.wagrown.com/recipes/speedy-blender-salsa/?gclid=Cj0KCQjwqoibBhDUARIsAH2OpWgnhIP0pynFfnoWVMPgp81ohgWpH04SRuzgBQMjVPCFZC8CIKuKPv8aAndQEALw_wcB).
```
 let salsa = Salsa { 
        tomatoe: 3, 
        lime_juice: "1 TBSP".to_string(), 
        cilantro_leaves: "1/3 Cup".to_string(), 
        salt: true, 
        tabasco: true,
    };
```
### It's Serde Blending Time 🔥🔥🔥🔥

![](https://i.imgur.com/i6ekA3p.png)

In this example, when I say blending, I really mean serialization. In order to turn a rust data structure into a JSON string, we have to use our serde crate and pass in our sala structure. 

**DUMP THOSE WASHINGTON GREEN INGREDIENTS INTO YOUR LOVELY TOASTMASTER BLENDER THAT YOU BOUGHT FROM AMAZON ! ! !**

`let json_str = serde_json::to_string(&salsa).unwrap();`

TURN ON THE BLENDER!
Type the following print statement to serialize your new salsa serde recipe.

`println!("Serialize: {}", json_str);`

We declared a new structure named `json_str` to denote that this will turn our salsa struct into a JSON string. First we pointed the `serde_json` function at our salsa, and then we recieved our type string instance by unwrapping it which then allows us to print the string. 

---
### Run your code : Part 1 ✨
it's time to see how our salsa serde turned out. 

Open your command line in VS Code [`^`+`~`] and run the following command. 
` $ cargo run`

You should see a return value that looks like this. 
```
Serialize: {"tomatoe":3,"lime_juice":"1 TBSP","cilantro_leaves":"1/3 Cup","salt":true,"tabasco":true}
```

You have successfully returned a JSON string from a Rust structure. 

I hope it tastes good :100: 

---

## How do we deserialize a string back into a rust structure?

In real life, it wouldn't be possible to turn salsa back into it's original ingredients. However, Salsa Serde is magical ✨

Back in our code editor bellow the serialization structure, write the following line of code to do the unfathomable. 

`let work_from_json: Salsa = serde_json::from_str(json_str.as_str()).unwrap();`

As before, we create a new structure named `work_from_json` and orient its type as `Salsa`. 
We want Serde to map the values in our serialized `json_str` from a JSON model to a Rust Struct. To make that happen, we tell our `from_str` method to pass the `json_str.as_str()` as an argument. We then have to unwrap it to return the appropriate Rust data structure.

It's time to see some magic happen! Type the following print method to see your deserialized salsa recipe transform back into it's origial `Salsa` structure.

`println!("Deserialize: {:?}", work_from_json);`

---

### Run your code :  Part 2 ✨
`$ cargo run`

###### 🪄 Abracadabra - Salsa Serde Reverse! 

You should see the following output in your Terminal.
`Deserialize: Salsa { tomatoe: 3, lime_juice: "1 TBSP", cilantro_leaves: "1/3 Cup", salt: true, tabasco: true }`

---
### How can we organize the format of our structures?

You have successfully made the worlds best Salsa Serde. The entire family can't stop dipping their tostito chips in your Salsa Serde, and now it's all gone! They demand you write the recipe on a stone tablet to harness the great magical powers of the Salsa Serde. 

In order to format a serialized JSON structure, we will need to implement a standard format to properly display the Salsa Recipe. 

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
Here you can see we've created a function `fmt` to accept two arguements that will accept existing public varibles related to the Serialized Salsa Recipe, and a **mutable** field of the values being passed. We want to return a **formated** string containing the results of our serialized JSON salsa recipe and `write!` it on the stone tablet ("Terminal").

**Back in our Main function**: 
Go to the bottom of body of the main function and write the same line of of code you did for `work_from_json`, without `{:?}`

```
let work_from_json2: Salsa = serde_json::from_str(json_str.as_str()).unwrap();
    println!("Deserialized V2: {}", work_from_json2);
```
Since we are not debugging our recipe, there is no need for `:?`

---

### Run your code : Part 3 ✨

![](https://i.imgur.com/SngW46h.png)
![](https://i.imgur.com/KR30JW0.png)  By the holy light... The Salsa Serde has finally arrived.

---

### Final words
I hope this Tutorial was fun for you to go through. Serde is a powerful tool with many other features that you should take the time to explore in depth for your own project. It's the perfect library for formating data you recieve from API's for real time web applications.
