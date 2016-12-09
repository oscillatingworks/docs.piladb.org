# Getting Started

## Preface

The main purpose of **piladb** is to be easy to understand, and easier to use. If you are trying to get started and you failed, don't blame yourself, we didn't do our job correctly!

Before installing **piladb**, it's worth to mention that it was designed and developed with **Linux** systems in mind. Although, compatibility and first class support for **macOS** is guaranteed, and it will stay like this forever. Said this, **piladb** should work on **Windows** too, yet there's not official support as of now.

## What is piladb?

**piladb** is a database engine, which means that it's a tool that provides mechanisms to store data in a certain way. In the case of **piladb**, this way is by piling data **_Elements_** in **_Stacks_,** so you only have access to the _Element_ on top, keeping the rest of them underneath. 


A **_Stack_** represents a linear data structure that contains _Element on the LIFO (_Last in, First out_) principle and in which only this operations are allowed:

* **PUSH**: Introduce an Element into the Stack. 
* **POP**: Removes the topmost Element of the Stack.
* **PEEK**: Returns the topmost element of the Stack, but this is not modified.
* **SIZE**: Returns the size of the Stack.
* **FLUSH**: Delete all Elements of the Stack, leaving it empty.

An **_Element_** is a piece of data that can be pushed into a _Stack_ and 

