# All About Serializing and Deserializing with Serde - A Primer

## What is Serde ?

According to the official website, “Serde is a framework for serializing and deserializing Rust data structures efficiently and generically”. But what does that mean? In the world of technology, there are various types of data structures. Data structures are just different ways to store something in a computer so it is optimized and efficient. When you have various data structures, a problem emerges. How do you transfer these data structures efficiently without messing them up?

This is where Serde comes in. Serde takes common Rust data types/structures and “serializes” or changes them into a format which can be sent or transferred easily. Serde also provides methods for “deserializing” or changing these formats back into the original data structure.

That was a brief intro to what Serde is and what it’s used for; in this tutorial, we will go deeper into all its cool features and how it can be used for various tasks.

---

## Serializing a struct to JSON

A wise man once said to build a deep understanding of something; one shall have tried it out themselves. So, let’s build a simple project showing how Serde works in Rust. I encourage you to follow along to understand these concepts.

Once a basic Rust project is set up, add the latest version of Serde to your dependencies by adding this line onto the Cargo.toml file. It imports version `1.0.147`

```Rust
serde = { version = "1.0.147", features = ["derive"] }

```

In this first example, let’s see how we can use Serde to serialize and deserialize a custom struct with a few parameters.

First, import the Serialize and Deserialize methods of Serde by adding this line to the top of our code:

```Rust
use serde::{Serialize, Deserialize};
```

Now let’s define a struct that can be serialized and deserialized.

In Rust, a `struct` stands for structure or a way to group many different values into a single type. Let’s define a structure that can be used to store the details of a student who is studying at school.

There can be many properties, like the student’s name, id, grade, etc. We can use the code below to do this.

```Rust
struct Student {
    id: i32,
    name: &str,
    grade: i8,
}
```

I will briefly explain this code.

We are creating a structure called `student`, with an `id` being a 32-bit integer, a name being a string, and a `grade` being an `8-bit` integer. We can use this structure to create many students following this pattern. We can insert this code just above our main function.

There is one thing we have to do before we can start serializing and deserializing objects using this structure. We need to generate the implementations necessary for completing these processes. Thankfully, Serde provides a `derive` macro to generate serialization implementations for structs. We can use the following code to do this:

```Rust
#[derive(Serialize, Deserialize, Debug)]
```

Place this code right above where you defined the `struct`, and it should do the magic.

So what exactly is this doing?

In simple terms, it generates the methods necessary to serialize the struct. Now, this `derive macro` is good and straightforward to use, but Serde also allows you to create your own custom serialize and deserialize traits, which we will get to later in this tutorial.

Anyways, let’s now make an object with this structure that we just defined. We can do that by using something like this:

```Rust
let mark = Student { id: 1, name: "Mark".to_string(), grade: 6 };

```

Here we are creating a new variable, `mark`, using the Student struct we created, and we set info about the student mark that we specified in the struct. Put this piece of code in your main function.

Now let’s see how we can turn this into a serialized string using Serde that can be transferred safely and efficiently. Serde can serialize/deserialize data structures into over 20 formats, thanks to the community.

In this tutorial, let’s see how we can serialize this data structure to JSON, which is one of the most popular data formats, especially used by JavaScript and web apps. To serialize to JSON, we need to install a new crate, `serde_json`. Add the below line to your Cargo.toml file to install the latest version of this crate.

```Rust
serde_json = "1.0.89"

```

After that, we can use this crate in our file by importing it. Add the below line of code to the top of your file.

```Rust
use serde_json;
```

Now let’s get to the actual fun stuff. Serializing and deserializing our text using Serde.

We have already set up the methods necessary to do this when we added the `derive` macro above our struct, so this should be a piece of cake. I will show the code to do this, then explain in detail what it’s doing.

```Rust
let serialized = serde_json::to_string(&mark).unwrap();
```

First, we are using the `to_string` method of the `serde_json` package. It is used to derive the serialized string of an object. We pass in the mark variable, since that is what we want to serialize.

Unwrap is a Rust function that is used to get the output of a function that can either return an error or an output. To explain this better, it simply “unwraps” the result of the JSON string to get just the value that we need.

Now for the moment of truth.

Did we actually serialize Mark into a JSON string? There’s only one way to find out:

```Rust
println!("initial = {:?}", mark);
println!("serialized = {}", serialized);
```

The above code prints the original student that we created, along with the serialized output that we got. If you followed the instructions properly, you should’ve got something like this:

```Rust
initial = Student { id: 1, name: "Mark", grade: 6 }
serialized = {"id":1,"name":"Mark","grade":6}

```

Notice how the initial version says Student before it. That shows that the output is actually a child of the structure. On the other hand, the serialized output is a lot more condensed and shows as a string.

---

## Deserializing a struct to JSON

Now serializing a struct is great, but how can we convert our string back into a Student. This is useful for transferring data between multiple Rust servers, having the data sent as JSON, but using Serde it can then be converted back into the original struct.

Using Serde, this is not hard at all. This can be achieved with just one line of code:

```Rust
let deserialized: Student = serde_json::from_str(&serialized).unwrap();
```

It’s very similar to the first logic, we use the `from_str` method and unwrap it, and store it to a “deserialized” variable on which we set the type as Student. Now let’s see if it is the same as the original student we created.

```Rust
println!("deserialized = {:?}", deserialized);
```

If it worked properly, you should have an output like this:

```Rust
initial = Student { id: 1, name: "Mark", grade: 6 }
serialized = {"id":1,"name":"Mark","grade":6}
deserialized = Student { id: 1, name: "Mark", grade: 6 }

```

Notice how the deserialized output is identical to the initial output. This is the essence of the Serde framework.

Code for this part of the tutorial:
You can click this [link](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021&gist=2025a03432156d1d6e385f5d677521ac) to test it out in a Rust Playground

```Rust
use serde::{Deserialize, Serialize};
use serde_json;


#[derive(Serialize, Deserialize, Debug)]
struct Student {
    id: i32,
    name: String,
    grade: i8,
}

fn main() {
    let mark = Student {
        id: 1,
        name: "Mark".to_string(),
        grade: 6,
    };

    // Convert the Point to a JSON string.
    let serialized = serde_json::to_string(&mark).unwrap();
    let deserialized: Student = serde_json::from_str(&serialized).unwrap();

    println!("initial = {:?}", mark);
    println!("serialized = {}", serialized);
    println!("deserialized = {:?}", deserialized);

}
```

Now that we have covered the basics, let’s see some of the more advanced features of Serde.

---

## Attributes

The derive we saw creates implementations for Serializing and Deserializing objects. For customizability, Serde also provides attributes which can be used to modify these auto-generated implementations.

You can use these by putting the attribute right below the derive line.

For example, this is how we serialize a `Person` struct, using an attribute to convert all the parameters to camel case.
You can click this [link](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021&gist=503d6a0493159fe8fdd56fac0113a402) to test it out in a Rust Playground

```Rust
use serde::Serialize;
#[derive(Serialize)]
#[serde(rename_all = "camelCase")]
struct Person {
    first_name: String,
    last_name: String,
}

fn main() {
    let person = Person {
        first_name: "Graydon".to_string(),
        last_name: "Hoare".to_string(),
    };

    let json = serde_json::to_string_pretty(&person).unwrap();

    // Prints:
    //
    //    {
    //      "firstName": "Graydon",
    //      "lastName": "Hoare"
    //    }
    println!("{}", json);
}
```

Notice how there is a line right below the derive line that specifies the attribute. There are many different attributes like these in Serde, but the process of using them is the same as the one shown above. Here is a link to see about the other attributes in Serde.

https://serde.rs/attributes.html

---

## Custom serialization/deserialization

Great we learned about how to serialize and deserialize using the built in derive implementation, and how to further customize this process via attributes, but there is one more step that gives us the ultimate control over the process. - **Custom Serialization**.

This allows us to customize how the serialize and deserialize traits are implemented to design our own logic.

```Rust
pub trait Serialize {
    fn serialize<S>(&self, serializer: S) -> Result<S::Ok, S::Error>
    where
        S: Serializer;
}
```

For example, this is the Serialize trait. It looks overwhelming at first, but it’s actually very simple. It’s goal is to take a `&self` variable, and map it into Serde’s data model.

Now you may ask, what the heck is a Serde data model?!

It’s basically a collection of types Serde uses internally to do it’s magic. There are 29 types which are in this model, primarily types that Rust supports by default. You can view the list here: https://serde.rs/data-model.html#types

So our goal with the custom serialization is to take the self variable and turn it into a format that’s supported by the Serde data model internally. For a lot of basic Rust types, Serde provides methods to handle this simply. For example, we can create a custom serializer for our Student struct we created earlier like this:

```Rust
use serde::ser::{Serialize, Serializer, SerializeStruct};

struct Student {
    id: i32,
    name: &str,
    grade: i8,
}

impl Serialize for Student {
    fn serialize<S>(&self, serializer: S) -> Result<S::Ok, S::Error>
    where
        S: Serializer,
    {
        // 3 is the number of fields in the struct.
        let mut state = serializer.serialize_struct("Student", 3)?;
        state.serialize_field("id", &self.id)?;
        state.serialize_field("name", &self.name)?;
        state.serialize_field("grade", &self.grade)?;
        state.end()
    }
}
```

Deserialization works the exact same way, but it’s a bit more complicated. The deserializer provides methods such as

```Rust
deserializer.deserialize_i32(I32Visitor)
```

For deserialization, we also need to implement a Visitor that’s used to create an object with the structure. Here is an example for a custom serializer, deserializer and visitor for a custom map with 2 fields.

You can run this code to see the output yourselves. Click this [link](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021&gist=d6c85fb062640253121f0b9c42479d74) to test it out in a Rust Playground

```Rust
use serde::ser::SerializeMap;
use serde::{Serialize, Serializer, de::Visitor, de::MapAccess, Deserialize, Deserializer};
use std::fmt;

#[derive(Debug)]
struct Custom(String, u32);

impl Serialize for Custom {
    fn serialize<S>(&self, serializer: S) -> Result<S::Ok, S::Error>
    where
        S: Serializer,
    {
        let mut seq = serializer.serialize_map(Some(2))?;
        seq.serialize_entry("first", &self.0)?;
        seq.serialize_entry("second", &self.1)?;
        seq.end()
    }
}

impl<'de> Deserialize<'de> for Custom {
    fn deserialize<D>(deserializer: D) -> Result<Self, D::Error>
        where
            D: Deserializer<'de>
    {
        deserializer.deserialize_map(CustomVisitor)
    }
}

struct CustomVisitor;

impl<'de> Visitor<'de> for CustomVisitor {
    type Value = Custom;

    fn expecting(&self, formatter: &mut fmt::Formatter) -> fmt::Result {
        write!(formatter, "a map with keys 'first' and 'second'")
    }

    fn visit_map<M>(self, mut map: M) -> Result<Self::Value, M::Error>
    where
        M: MapAccess<'de>
    {
        let mut first = None;
        let mut second = None;

        while let Some(k) = map.next_key::<&str>()? {
            if k == "first" {
                first = Some(map.next_value()?);
            }
            else if k == "second" {
                second = Some(map.next_value()?);
            }
            else {
                return Err(serde::de::Error::custom(&format!("Invalid key: {}", k)));
            }
        }

        if first.is_none() || second.is_none() {
            return Err(serde::de::Error::custom("Missing first or second"));
        }

        Ok(Custom(first.unwrap(), second.unwrap()))
    }
}


fn main() {
    let stru = Custom("abc".to_string(), 123);
    println!("Orig {:?}", stru);

    let serialized = serde_json::to_string(&stru).expect("error while serializing");

    println!("Seri {}", serialized);

    let unse : Custom = serde_json::from_str(&serialized).expect("err while deserializing");
    println!("New {:?}", unse);
}
```

I will explain this code briefly. We have a `struct` which is basically a map of 2 things, a `string` and an `unsigned 32 bit integer`. Notice how the `derive` keyword is present, but doesn’t contain the Serializer and Deserializer. This is so that Serde doesn’t automatically generate implementations for us. Below, we have our custom serializer.

Our custom serializer serializes the first and second values of this map, using the key words “first” and “second”. It uses the serialize entry method which is used for Maps.

The deserializer is a bit more complicated. We have a built in deserializer function for maps, which is great, but we then have to create the Visitor that will actually create the object when deserializing.

It has an expecting function which sends an error if the serialized output isn’t formatted right. Then we have the actual deserializer itself, it loops through each value in the serialized output checking for the `first` and `second` keywords, and at the end we see that it sends an Ok response with a new Custom struct using the first and second values.

Then, in the main function of the program, we just create a new object using our `Struct`, and showcase the methods to **serialize and unserialize**. Note how it’s exactly the same as how we did it in the beginning of the tutorial.

---

## Conclusion

In this tutorial, I covered everything that you need to use Serde, and even some of the power user features that are used less. I hope you found this tutorial useful, and you learned something out of this.
