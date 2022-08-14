# RmbRT Programming language

![RmbRT-lang-chud](https://user-images.githubusercontent.com/12518378/184537409-a47a6add-1056-4092-8114-67d76a7a0cfe.png)

The RmbRT programming language is pronounced as "rmbrt" (chinks and burgers BTFO).

Coming soon. I'm currently rewriting the standalone compiler to be more easily maintainable and extendable.

* You can already use the [`bootstrap compiler`](https://github.com/RmbRT-lang/rmbrtbc) to compile RmbRT programs, but it's still a bit buggy due to technical limitations (such as using C++ as the intermediate language).
* See [`rmbrtc`](https://github.com/RmbRT-lang/rmbrtc) and [`std`](https://github.com/RmbRT-lang/std) to get an impression of what the language is like.

## Mission

RmbRT language is intended to be a programming language for *experts*.
It aims to fulfill the following features:

* Great performance,
* compact & readable code (only if you are an expert, albeit),
* simple syntax,
* expressive mechanisms for using higher abstractions and concurrency.

It is designed to allow writing clean, expressive, and safe code, without being overly academic or annoying.
Its simple syntax and higher level concepts are intended to allow for easy development of additional tooling such as analyzers and model checkers.

## NOT Mission

* Compatibility with existing software stacks.
* Compromises in the design.
* Backwards compatibility.
* Corporate use.
* POSIX compliance/compatibility.

## (Preliminary) Roadmap

1. Feature-complete stand-alone compiler (rmbrtc) for executables.
1. RmbRT ASM object files, ahead-of-time template compilation, pre-compiled project dependencies/libraries.
1. Full debugging support.
1. Full language documentation.
1. Decentralised code repositories.
1. Decentrally attested compilation.
