# ncc

NCC is a new compiler suite, the compilers will be similar to the Plan 9
compilers, with separate compilers for different architectures. The compilers
implement ANSI C with restrictions and improvements. The aim is to bring a
new way to write C programs that can be written and compiled easily across
architectures and operating systems.

## Standard Library

The standard library is the most outstanding feature in ncc as it is completely
different to the ANSI C and POSIX libraries commonly used. The standard library
takes heavy inspiration from the [Go stdlib](http://golang.org/pkg/), the most
important being the os and syscall packages, the implement the routines that
interact with the system, and they do it in an extremely clean way that enables
easy cross compatibility while still allowing routines specific to one OS. Of
course some of the common routines like `malloc/free` and other pretty important
routines will be implemented as well.

## Assembler

The assembler used to compile any assembly routines is similar to NASM, and may
be written with either AT&T or Intel syntax which is detected once the assembly
process starts.

## Builder Program

`cbuild` is a builder that makes it easy to compile projects. The following are
a set of outstanding features the builder includes:
- `#!` Support in source files. It will link then execute a program, and
discard it's executable afterwards.
- Smart compiling to make it easier to build programs with system dependent
features. Details below.
- Easy cross platform building.

### Usage

Examples:

```
cbuild -o main main.c
# Compile and link main.c to main.

cbuild -o main main.c dep.o
# Compile and link main.c including the object dep.o and write to main.

cbuild -c -o main.o main.c
# Compile main.c to the object main.o.

cc -o project project
cc -c -o project.o project
# The following use the smart compilation feature for files prefixed with
# "project".
```

### Smart Compilation

Smart compile, compiles source files that include a given prefix. It makes it
easy to include source files that are only compiled for specific platforms.

`cbuild` contains arguments to change the output OS/arch, and if they're not
given the default is the OS/arch `cbuild` was compiled for. Below are a list of
possible OS/arch options supported.

Source files may contain a build comment that restricts the OS/arch that may
build it. The format is `build: OS,arch !OS,arch`, where OS/arch are separated
by spaces, and the arch is optional. To disallow an OS/arch, prefix it with `!`.
e.x.: `/* build: bsd, !darwin */` Will allow all BSDs to build it except darwin.

Source files may be written in C(`.c`) or Assembly(`.s`, `.asm`).

When using smart compilation any file with the prefix is gathered and processed
to determine which are going to be compiled. The following are the possible file
formats:

- `prefix.*` This file is always compiled(if not restricted by build
comments). It should be used for general routine implementations.
- `prefix_{OS}.*` This file is only built if the OS var is satisfied by the
output OS(and not restricted by build comments).
- `prefix_{OS}_{ARCH}.*` This file is only built if the OS and ARCH vars are
satisfied by the output formats(and not restricted by build comments).

If multiple satisfied OS files are found, the most specific for the output is
used.

### OS/arch options

- `darwin`
- `linux`
- `windows`
- `freebsd`
- `openbsd`
- `netbsd`
- `dragonfly`
- `unix` The above unixes also fall into this category.
- `bsd` The above that are BSD also fall into this category.

- `386`
- `amd64`
- `arm`
