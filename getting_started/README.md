# Getting Started

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

A **_Database_** is an entity that contains _Stacks_. So every _Stack_ belongs to a _Database_.

We'll know as **_Pila_** the super object that will contain and handle all _Databases_, _Stacks_ and _Elements_, as well as memory management, session handling and concurrent operations requests.

**`pilad`** is the daemon program, or server, that will initialize the _Pila_,  exposing to external users an Interface to iterate with it: create _Databases_, create _Stacks_, `PUSH` or `POP` _Elements_, etc.