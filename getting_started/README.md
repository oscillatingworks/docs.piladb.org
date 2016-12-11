# Getting Started

## Preface

The main purpose of **piladb** is to be easy to understand, and easier to use. If you are trying to get started and you failed, don't blame yourself, we didn't do our job correctly! Please report an issue into [the repo](https://github.com/oscillatingworks/pilabook/issues) and tell us what's not right.

Before installing **piladb**, it's worth to mention that it was designed and developed from a **Linux** OS for **Linux** OS's. Although, compatibility and first class support for **macOS** is guaranteed, and it will stay like this forever. Said this, **piladb** should work on platforms like **Windows** or *BSD too, yet there's not official support as of now.

## What is piladb?

**piladb** is a database engine, which means that it's a tool that provides mechanisms to store data in a certain way. In the case of **piladb**, this way is by piling **_Elements_** in **_Stacks_,** so you only have access to the _Element_ on top, keeping the rest of them underneath. 

### Basic concepts

An **_Element_** is a piece of data that can be pushed into a _Stack_, and has a JSON compatible format. This means that you can handle in **piladb** the following data types:

* Number: `42`, `3.14`, `.333`, `3.7E-5`.
* String: `foo`, `PilaDB`, `\thello\nworld`, ` `, 💾.
* Boolean: `true`, `false`.
* Array: `["🍎","🍊","🍋"]`, `[{"foo":false}, true, 3, "bar"]`.
* Object: `{}`, `{"key": "Value"}`, `{"bob":{"age":32,"married":false,"comments":{}}}`.
* `null`.

A **_Stack_** represents a linear data structure that contains _Elements_, based on the LIFO (_Last in, First out_) principle, and in which only these operations are allowed:

* **PUSH**: Introduces an Element into the Stack. 
* **POP**: Removes the topmost Element of the Stack.
* **PEEK**: Returns the topmost Element of the Stack, but this is not modified.
* **SIZE**: Returns the size of the Stack.
* **FLUSH**: Delete all Elements of the Stack, leaving it empty.

Every _Stack_ has a name and an unique identifier.

A **_Database_** is an entity that contains _Stacks_. So every _Stack_ belongs always to a _Database_. Two _Stacks_ cannot share the same name if they belong to the same _Database_. If they don't, they will still have unique identifiers, as they are generated based on the containing _Database_. A _Database_ also has a name and an unique identifier itself.

We'll know as **_Pila_** the super object that will contain and handle all _Databases_, _Stacks_ and _Elements_, as well as memory management, session handling and concurrent operations requests.

**`pilad`** is the daemon program, or server, that will initialize the _Pila_,  exposing to external users an Interface to iterate with it: create _Databases_, create _Stacks_, `PUSH` or `POP` _Elements_, etc.

Above all these concepts, **piladb** represents the most important one. It is a project written in [Go](https://golang.org), hosted on [Github](https://github.com/fern4lvarez/piladb), that implements all these ideas, plus others like a configuration module, resources to work with Docker, or another internal packages.