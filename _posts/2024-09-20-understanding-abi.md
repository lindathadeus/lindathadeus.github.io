---
layout: post
title: "Understanding ABI"
date: 2024-09-20
categories: linux
giscus_comments: true
tags: [linux, ABI]
---

When we compile and execute a program in Linux, it’s not just the source code interacting with the system directly. Instead, the ABI (Application Binary Interface) plays a crucial role in facilitating the communication between the program and the operating system. In this blog post, we'll dive into the key aspects of ABI through a practical example, a simple "Hello, World".

### Step 1: Writing and Compiling a Simple C Program

```bash
echo "#include <stdio.h>" > hi.c
echo "int main() {" >> hi.c
echo "  printf(\"Hello, World!\");" >> hi.c
echo "  return 0;" >> hi.c
echo "}" >> hi.c

gcc hi.c -o hi
```

The resulting binary is an ELF (Executable and Linkable Format) file, a standard format used in Linux systems. This file uses the ABI to interact with the OS when executed.

### Step 2: Key Responsibilities of the ABI

When the binary runs, the ABI ensures several key operations:

1. **Calling Conventions**: It defines how function arguments are passed—whether in registers or on the stack.
2. **System Calls**: The ABI manages the interactions between the binary and the OS, particularly how system calls are invoked.
3. **Binary Format**: The structure of the binary file, including sections like `.text`, `.data`, and `.bss`, is defined by the ABI.
4. **Linking**: It governs how dynamic or static linking is handled between the program and shared libraries, such as `libc.so`.

### Step 3: Inspecting the Binary

You can inspect the compiled binary using tools like `readelf` and `ldd`:

```bash
$ readelf -h hi
$ ldd ./hi
```

This shows the ELF header and dynamic library dependencies, respectively. For example:

```
linux-vdso.so.1 (0x00007ffe625f0000)
libc.so.6 => /lib/x86_64-linux-gnu/libc.so.6
/lib64/ld-linux-x86-64.so.2
```

### Step 4: Generating Assembly Code

To view the assembly equivalent of the C program, you can generate the assembly code:

```bash
$ gcc -S hi.c -o hi.S
$ file hi.S
```

This outputs the assembly source code, giving you insight into the low-level instructions that are executed.

### Step 5: ABI Compatibility

The ABI ensures compatibility across different Linux distributions, allowing binaries compiled on one system to work seamlessly on another. Here's a checklist of what the ABI manages:

- **Data Types**: Defines the sizes and alignment of data types like `int` and `long`.
- **Endianness**: Specifies the byte order in which data is stored.
- **System Calls**: Governs how to request services from the kernel.
- **Linkage Conventions**: Dictates how libraries are linked and called.

### Step 6: System Call Analysis

Using `strace`, we can analyze the system calls used by our simple "Hello, World!" program:

```bash
$ strace ./hi
execve("./hi", ["./hi"], 0x7dddeedbeef /* 53 vars */) = 0
brk(NULL)                               = 0x5bbdddeedbeef
arch_prctl(0x3001 /* ARCH_??? */, 0x7fdddeedbeef) = -1 EINVAL (Invalid argument)
mmap(NULL, 8192, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS, -1, 0) = 0x70dddeedbeef
access("/etc/ld.so.preload", R_OK)      = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/etc/ld.so.cache", O_RDONLY|O_CLOEXEC) = 3
...
```

The output reveals multiple system calls, even for a simple program:

- **execve**: Executes the binary.
- **openat**: Opens shared libraries.
- **write**: Outputs "Hello, World!" to `stdout`.
- **exit_group**: Terminates the program.

### Why So Many System Calls?

Even a basic program like this makes numerous system calls because:

- **Memory Management**: The OS needs to allocate memory for the program.
- **Library Linking**: The program relies on shared libraries like `libc`.
- **Resource Management**: The system must handle file descriptors, memory, and potentially threading.

### Conclusion

The ABI is essential for maintaining compatibility and ensuring that programs run correctly across different systems. Understanding how the ABI manages function calls, system interactions, and binary formats can deepen your knowledge of Linux programming and system operations. Even though a "Hello, World!" program appears simple, it triggers complex interactions behind the scenes, all managed by the ABI.

---

By exploring ABI, you gain a better understanding of how Linux systems work under the hood, making you a more effective developer.
