# Newt
Newt is a C-like general purpose language, providing imperative language features
and a strong static type system. It is designed to be a middle ground providing
some low level systems programming features and higher level features suited
for building applications.

Newt provides a suite of compilers for all the supported architectures and
provides a tool that uses them to build cross-platform code easily.

## Preprocessor
A preprocessor is included that provides macro expansion, source code inclusion,
and conditional compilation. A set of predefined macros are included by default
that make working with the target operating system easier.

The preprocessor language is simple and familiar to people that have worked with
the C preprocessor. All definitions are prefixed with "#" with the exception of
macro calls and operand expressions.

A spec for the preprocessor language is provided in the included "docs/" directory.

## Standard Library
The Newt standard library takes heavy inspiration from the Go stdlib, providing
a large collection of libraries for common things such as crypto, memory
management, encoding, data structures, networking, and much more.

Memory management is an important feature in any language, and Newt provides
multiple ways to manage it. Manual memory management is of course included so
you have complete control over any memory used, but if you don't need to control
every aspect of the memory use, a garbage collection library is included as well.

Newt also provides a common interface to all the supported operating systems,
making it simple to do the most common procedures on all of them. In the case
you need something more low level, libraries that provide operating system
specific features are included and well supported.

## Assembly
Newt also provides an assembler that can build code that is specific to architecture
and operating system. The raw compiler output is also in the same assembly syntax.

The preprocessor is ran on assembly code before the build begins, so you can
use the same macros, etc. as you would in Newt code.

A spec for the assembly syntax is provides in the incldued "docs/" directory.
