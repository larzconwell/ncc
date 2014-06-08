# newt

Newt is a new compiler suite, the compilers will be similar to the Plan 9
compilers, with separate compilers for different architectures. The compilers
implement ANSI C with restrictions and improvements. The aim is to bring a
new way to write C programs that can be written and compiled easily across
architectures and operating systems.

## Standard Library

The standard library is the most outstanding feature in newt as it is completely
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
