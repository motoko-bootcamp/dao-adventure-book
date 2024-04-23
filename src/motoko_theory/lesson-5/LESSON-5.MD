# Lesson 5: Modules

## 🧩 Modules

So far, we've explored the basics—operations like addition, subtraction, and string concatenation built directly into the language. To tackle more complex tasks, we'll need to delve into the world of modules.

Modules are collections of named variables, functions, and types, each designed for a specific purpose. They help us organize our code efficiently. Typically, a module resides in its own file, allowing us to import its contents into other Motoko files as needed.

Unlike the `main.mo` file, which begins with the `actor` keyword, a module starts with the `module` keyword.

```motoko
module {
    public func Utils() : async () {
        // This utility function can be imported elsewhere
    };
}
```

Modules enable you to define types, classes, or utility functions, which you can then import into your `main.mo` file.

## 📚 Base library

The base library comprises a collection of modules that offer functions for working with common data types like `Bool`, `Nat`, `Int`, `Text`, and others.

This library's source code is hosted on GitHub, with contributions from DFINITY foundation engineers and the wider community. Each module comes with its documentation page, detailing the functions it provides. For instance, you can find [the documentation page for the `Nat` module](https://internetcomputer.org/docs/current/motoko/main/base/Nat).

<p align="center"> <img src="assets/base_library_nat.png" width="800px" style="border: 2px solid black;"></p>
<p align="center">  </p>

To import from the base library, you use the `import` keyword, followed by the module's local name and a URL pointing to the module's location.

```motoko
import Buffer "mo:base/Buffer";
actor {
    let buffer = Buffer.Buffer<Text>(0);
};
```

Additionally, you can import Motoko code and other modules using relative paths. For instance, if you've created a program named `types.mo` in the same directory as your main program, you could include it with an import declaration like this:

```motoko
import Types "types";
actor {
    public type ExternalType = Types.ExternalType;
};
```

## 🐶 MOPS

MOPS is a Motoko package manager featuring a fully on-chain package registry. It allows you to install packages from the Motoko community in your projects.

<p align="center"> <img src="assets/mops.png" width="800px" style="border: 2px solid black;"></p>
<p align="center">  </p>

Here is the [quick start guide](https://docs.mops.one/quick-start) from MOPS.
