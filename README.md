# Nyxstone

The simple assemble/disassemble framework. Nyxstone was built as an internal software project for our powerful binary rewriter _NYX_. 

With Nyxstone we do not ship our own LLVM patches, but wrap LLVM `MC` objects in custom types to assemble and disassemble for
different architectures.

## Building
Building Nyxstone requires a modern compiler, we currently use `clang`. 

Nyxstone uses the LLVM backend to assemble & disassemble instructions. Since the LLVM backend changes frequently with major releases, we currently only support LLVM major version 15. 

When Nyxstone is being built, it first searches the directory supplied by the environment variable `$NYXSTONE_LLVM_PREFIX/bin` and afterwards the `$PATH` for `llvm-config`.  When `llvm-config` is found, Nyxstone checks for both the major version and if LLVM can be statically linked. 

There are multiple ways to install LLVM 15 if your package manager does not supply it:
 - Use an external package manager, like `brew`
 - Build llvm from source
 - Ubuntu/Debian only: Use the install script from https://apt.llvm.org

Also make sure to install any libraries needed by your LLVM version for static linking.

You can build the nyxstone cli (nstone) example program and the small sample program in the `examples` folder using cmake. Use the following commands:
```
$ mkdir build
$ cd build
$ cmake ..
$ make
```

## Using Nyxstone

### CLI Tool
The Nyxstone cli tool allows for on-the-fly assembling and disassembling from your command line.
```
$ cd build && cmake .. && make
$ ./nstone --help
Allowed options:
  --help                    Show this message
  --arch arg (=x86_64)      Architecture, one of: x86_64, armv6m, armv7m,
                            armv8m, aarch64
  --address arg (=0)        Address

Assembling:
  --labels arg              Labels, for example "label0=0x10,label1=0x20"
  -A [ --assemble ] arg     Assembly

Assembling:
  -D [ --disassemble ] arg  Byte code in hex, for example: "0203"
```

### In your project
Currently, Nyxstone is only in use as a rust library via the rust bindings. If you want to use Nyxstone in your project, see the Makefile for how Nyxstone is build and how to link it into your projects.
