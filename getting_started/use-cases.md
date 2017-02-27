# Use Cases

Now that you know how to install and use **piladb**, you might be wondering what can you use it for. There's not a specific answer for that, **piladb** provides a very specific way of storing data, based on Stack data structures, and feeding and consuming this data, through a REST API in atomic operations. Given this, you can analyze your needs, requirements and architecture specs, and find a right use case for it.

In this article, we will explain some possible use cases that can help you understand why and when to use **piladb**.

## Caching System

A caching system can help you to save those pieces of data that are expensive to read, but you need to access frequently, so you can request them in a much faster way. These are for example complex queries to databases, requests to HTTP APIs or web scraping. **piladb** can be the caching system you need:

* If you push a _cached_ element on a Stack, it will be stored on top, so all reads will have constant complexity.
* You can store JSON documents, strings, HTML code, numbers, and more, which gives a lot of flexibility to cache data of different nature.
* Using multiple **piladb**'s Databases lets you split your cached data by categories or domains, so your cache is well organized.
* Requests to cached data are HTTP based, so if you avoid big latency between consumer and server, you get a standard and fast way to access the cache.

## Key-Value Store

A key-value store is a system where you store data, i.e. a value, associated to a key. So if you want to access these values, you do it with a lookup through their keys. This is very often used for storing configuration values or sharing such configuration between external services.

**piladb** can serve for this purpose, given that each Stack is a _key_ and its element on top is the _value_. A lookup into a key-value entry would consist on a simple `PEEK` operation. Furthermore, **piladb** can store older versions of a value, as elements on the Stack.

## Undo/Redo User Actions

Imagine you have a product based on user actions, e.g. an interactive web application, or a graphics editor. You want to keep track of these user actions, so they can easily be recorded and reproducible, and be undone or redone without restrictions.

For this use case, you can make your application to rely on **piladb** to store all user/session activities and implement a simple logic around it to implement the undo and redo of actions. You can have two Stacks: one to store _done_ activities, another for _undone_ activities. When doing _Undo_, you move the last _done_ activity to _undone_, and vice versa for _Redo_ actions.

## Message processing

If you need to enable async communication between two services, message processing approaches like Pub/Sub are a very common pattern. In this context, a publisher write messages in a _repository_ that subscribers read and consume, based on events, periodical requests or similar.

With **piladb** we can implement a message processing system, by making one or multiple services to be publishers, doing `PUSH` operations over a Stack, having other services as subscribers, consuming the messages with `POP` operations. Also, we can create different topics using multiple Stacks.

## More?

If you found new uses for **piladb**, please share them with us! You can [create an issue or PR](https://github.com/oscillatingworks/docs.piladb.org/issues/new) into our documentation repository.
