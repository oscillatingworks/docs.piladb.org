# Use Cases

Now that you know how to install and use **piladb**, you might be wondering what can you use it for. There's not a specific answer for that, **piladb** provides a very specific way of storing data, based on Stack data structures, and feeding and consuming this data, through a REST API in atomic operations. Given this, you can analyze your needs, requirements and architecture specs, and find a right use case for it.

In this article, we will explain some possible use cases that can help you understand why and when to use **piladb**.

## Undo/Redo User Actions

Imagine you have a product based on user actions, e.g. an interactive web application, or a graphics editor. You want to keep track of these user actions, so they can easily be recorded and reproducible, and be undone or redone without restrictions.

For this use case, you can make your application to rely on **piladb** to store all user/session activities and implement a simple logic around it to implement the undo and redo of actions.

### Context

A user is editing an image. He does these actions:

* Extend the canvas (action A)
* Paint some part in blue color (action B)
* Paint another part in black color (action C)

They don't like the result of painting in the canvas (B and C), so they undo _twice_, in order to come back to the status after the canvas was extended (A).

Then, the user decides that the blue color was fine (B), but wants to keep painting another parts with another colors and discard the black one (C).

### Solution

TBC
