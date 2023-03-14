# HOP

High-Order Virtual Machine Plus - A simple syntax layer on top of raw HVM, written in HVM.

Right now it's more like an HVM preprocessor, and all it does is resolve `#include` statements so that you can write HVM programs directly in multiple different files.

It's my first attempt at actually writing a functional program, and is for the most part a learning experiment for now. The full implementation is in [`hop.hvm`](./hop.hvm).

I know you're not really supposed to write HVM, but maybe this could still turn into a semi-writable version of HVM. I mean, even raw HVM is super expressive!

> **Note:** Currently requires this HVM [fix](https://github.com/HigherOrderCO/HVM/pull/217) to run.

## Features

### Multi-threaded!

This is a pseudo feature that feels worth pointing out. All I did was write a simple program, and it's already multi-threaded and resolves imports in parallel due to the amazingness of HVM. 🥳

### Hash tags

#### `#include`

Grab another hop file, compile it, and replace the include statement with it.

## Example

First we have a couple files.

**`option.hop`**

```dart
// This file could include another file if you wanted
// #include something.hop

(Option.map (Option.some x) map) = (Option.some (map x))
(Option.map (Option.none) map) = (Option.none)

(Option.unwrap_or (Option.some x) default) = x
(Option.unwrap_or Option.none default) = default
```

**`hello.hop`**

```dart
// Include Option.hop
#include option.hop

// Not actually a useful program
Main = (Option.unwrap_or (Option.some 1) 2)
```

Now we compile `Hello.hop` to `Hello.hvm`.

```bash
$ hvm run -f hop.hvm '(Main "hello.hop" "hello.hvm")'
(Done)
```

And now we get `hello.hvm`:

```dart
(Option.map (Option.some x) map) = (Option.some (map x))
(Option.map (Option.none) map) = (Option.none)
(Option.unwrap_or (Option.some x) default) = x
(Option.unwrap_or Option.none default) = default

// Not actually a useful program
Main = (Option.unwrap_or (Option.some 1) 2)
```
