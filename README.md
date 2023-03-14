# HOP

High-Order Virtual Machine Plus - A simple syntax layer on top of raw HVM, written in HVM.

Right now it's more like an HVM preprocessor, and all it does is resolve `#include` statements so that you can write HVM programs directly in multiple different files.

It's my first attempt at actually writing a functional program, and is for the most part a learning experiment for now. The full implementation is in [`hop.hvm`](./hop.hvm).

> **Note:** Currently requires this HVM [fix](https://github.com/HigherOrderCO/HVM/pull/217) to run.
