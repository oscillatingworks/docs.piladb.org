# Getting Started

## What is piladb?

**piladb** is a database engine, which means it's a tool that provides mechanisms to store data in a certain way. In the case of **piladb**, this way is by piling **_Elements_** in **_Stacks_,** so you only have access to the _Element_ on top, keeping the rest of them underneath.

### Basic Concepts

An **_Element_** is a piece of data that can be pushed into a _Stack_, and has a JSON compatible format. This means that you can handle in **piladb** the following data types:

* Number: `42`, `3.14`, `.333`, `3.7E-5`.
* String: `foo`, `PilaDB`, `\thello\nworld`, ` `, 💾.
* Boolean: `true`, `false`.
* Array: `["🍎","🍊","🍋"]`, `[{"foo":false}, true, 3, "bar"]`.
* Object: `{}`, `{"key": "Value"}`, `{"bob":{"age":32,"married":false,"comments":{}}}`.
* `null`.

A **_Stack_** represents a linear data structure that contains _Elements_, being compatible with both LIFO (_Last in, First out_) and FIFO (_First in, First out_) principles, and in which only these operations are allowed:

* **PUSH**: Introduces an Element on top of the Stack.
* **BASE**: Introduces an Element at the bottom of the Stack.
* **POP**: Removes the topmost Element of the Stack.
* **PEEK**: Returns the topmost Element of the Stack, but this is not modified.
* **FLUSH**: Delete all Elements of the Stack, leaving it empty.
* **ROTATE**: Moves the bottommost Element on top of the Stack.
* **BLOCK**: Blocks mutable operations on the Stack.
* **UNBLOCK**: Allow mutable operations on the Stack.
* **SIZE**: Returns the size of the Stack.
* **EMPTY**: Returns whether the Stack is empty.
* **FULL**: Returns whether the Stack reached the size limit when this is set.

Every _Stack_ has a name and an unique identifier.

A **_Database_** is an entity that contains _Stacks_. So every _Stack_ belongs to a _Database_.

We'll know as **_Pila_** the super object that will contain and handle all _Databases_, _Stacks_ and _Elements_, as well as memory management, session handling and concurrent operations requests.

**`pilad`** is the daemon program, or server, that will initialize the _Pila_,  exposing to external users an Interface to iterate with it: create _Databases_, create _Stacks_, `PUSH` or `POP` _Elements_, etc.

### Database Model

As of now, **piladb** writes into memory only, using a thread-safe model, and runs as a single server. This means that it doesn't persist data on disk and is not able to replicate its content to other **piladb** instances. If the server is shutdown, all data is flushed after giving a time to pending operation to finish.

Every operation applied to a **Stack** has a O(1) complexity, and will block further incoming or concurrent operations, which ensures consistent responses within a reasonable amount of time.

