# RmbRT Programming language

The RmbRT programming language is a Christian programming language, in that it seeks to fulfill the virtues that Yahweh our God likes:
* to take joy in the Word, to make speaking and reading the truth and wisdom pleasant,
* to not touch the unclean, I tried my best to create something pure.
* to take joy and comfort in your toil and to labour for things that satisfy,
* to dedicate the works of your hands to honour Yahweh; I hope that this language will be respected and that all the honour will be credited to Yahweh.

It is pronounced as "rmbrt" (no vowels, German "r").
Just deal with it, I'm not going to rename it.
If you have to, just call it RL instead.

If you use this language for the glory of God and lawful purposes, may you be blessed in the works of your hands.
If you use this language for lawless and evil purposes, may you be cursed with AIDS and monkeypox and evil spirits and demons.
Only use this language if you are a Christian – don't defile what another man dedicated to the glory of God.

This blessing and this curse are above your stupid licenses and mortal laws so don't even try to get around that, God is not tricked.

## Why use RL over C/C++, in one simple picture

![RmbRT-lang-chud](https://user-images.githubusercontent.com/12518378/184537409-a47a6add-1056-4092-8114-67d76a7a0cfe.png)

*Do you find this obscene? The real obscenity are bad programming languages!*

## Status

More information and documentation coming soon. I'm currently rewriting the self-hosted compiler to be more easily maintainable and extendable.

* You can already use the [`bootstrap compiler`](https://github.com/RmbRT-lang/rmbrtbc) to compile RmbRT programs, but it's still a bit buggy due to technical limitations (such as using C++ as the intermediate language).
* See [`rmbrtc`](https://github.com/RmbRT-lang/rmbrtc) and [`std`](https://github.com/RmbRT-lang/std) to get an impression of what the language is like.

## Mission

RmbRT language is intended to be a programming language for *experts* who love their craft.
It aims to fulfill the following features:

* Great performance,
* compact & readable code (only if you are an expert, albeit),
* simple syntax,
* expressive mechanisms for using higher abstractions and concurrency.
* timeless:
  must be usable for centuries without getting old. That's why I will be improving on it and fixing things until it can survive the ages.
  I am sick of seeing these half-baked programming languages that are a pain to use and who force false conceptions of computers on you.

It is designed to allow writing clean, expressive, and safe code, without being overly academic or annoying.
Its simple syntax and higher level concepts are intended to allow for easy development of additional tooling such as analyzers and model checkers.

## NOT Mission

* Compatibility with existing software stacks.
* Compromises in the design.
* Backwards compatibility.
* Corporate use.
* Lawless use.
* POSIX compliance/compatibility.

## (Preliminary) Roadmap

1. Feature-complete self-hosted compiler (rmbrtc) for executables. (currently WIP, expected by the end of 2024, Yahweh willing).
1. RmbRT ASM object files, ahead-of-time template compilation, pre-compiled project dependencies/libraries.
1. Full debugging support.
1. Full language documentation.
1. Decentralised code repositories.
1. Decentrally attested compilation.

# Glimpse into RmbRT language

So, I can give a short overview already to tease some features (some details may be subject to change):

* Reference constraints: passing a mutable reference is an explicit action, const references are the default behaviour. References overlapping in lifetime with a mutable reference become shared / volatile during that time. References overlapping in lifetime with references in other threads become atomic during that time, if at least one mutable reference exists. References cannot be converted to pointers. References cannot be stored, so their lifetime cannot be extended (this guarantees that side-effects remain constrained to the function a mutable reference was passed to).
* Native coroutine and thread support: `@call()` will return a coroutine promise, while `^call()` will return a thread promise. Promises have to be stored somewhere, and are implicitly awaited on destruction. Keep track of your processes. The handles to threads and coroutines can also be used to talk to them (kill etc.).
* Breaking the black-box: while abstract classes or union types are by default black-boxed, you can break the black-box using `>>(...)`, which basically executes the whole expression in a type switch. Using the object in a way that is not compatible with the run-time type will result in a run-time error. The `>>` operator can also be used on types, and can be used to create packed arrays of polymorphic types (no more pointer chasing).
* Error recovery: the `?` operator aborts an expression from within if the left-hand side results in a falsy value, and replaces it with `FALSE`, and this process escalates until the outermost expression is reached, or an `OR` operator is reached, which will then substitute the right-hand side of the `OR` operator with the failed left-hand side expression. If the left-hand side of `?` does not throw or evaluate falsy, it becomes the result of the `?` operation. It is legal to submit differing types on both sides of the `OR`, both sides can result in different overloads being called in the surrounding expression. Example: `print(:hex(SharedCounter?->Value) OR "No counter");`. The `OR` operator can also be used without the `?` operator, it will attempt to convert the left-hand side into a boolean, and if that is possible, replace it if it evaluates to false. Regardless of that, it will also swallow any exceptions thrown by the left-hand side and then do the expression substitution.
* Easy value unwrapping: the `!` postfix operator recursively unwraps objects. Specifically, if the returned type from the `!` operation also defines the operator, that is also called automatically. For types that do not have this operator, it becomes the identity function.
* Fast overloads: Not all operations are overloadable, there are some defaults that cannot be changed (for example, the assignment operator, or the unary `+`). Functions can be overloaded, but all but one version must have a unique name (`overloaded()` and `overloaded name(...)`). Values can be symbolically tagged, by writing `:symbol(value)`, which can then be passed to an overloaded function or constructor, and the symbolic name is used to look up the overload (logarithmic complexity for overload resolutions, as opposed to combinatoric complexity). If no such overload exists, the default overload is attempted to match. Constructors are overloaded the same way, and you can construct a variable as such: `f: File := :read("path");` (where `:read` is the constructor name).
