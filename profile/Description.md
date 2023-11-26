The Project Description
=======================

Today, almost all computer programs are not 100% self-sufficient.  They depend on libraries of code, written by other people, to do their work.  When a computer program is written, the compiler and linker work together to resolve which libraries and functions inside each library the program needs.  Later, when the program is run, a loading program finds the library files and "lazily binds" the libraries to the running program.  All of this happens in a common area of memory for the process called a "virtual address space".  Once a library joins this common virtual address space, it can access all of the memory in it.  There is no way for a program to keep a secret from a library.  Furthermore, there is no way for a program, running in this common virtual address space, to keep secrets from the computer’s components such as the operating system, hypervisor, or System Management Module.

In addition to this, most programs never have the opportunity to make decisions about which libraries are bound to it.  They can't tell if they come from trustworthy sources or if they have been tampered with.  So, programs that you run today, like your browser or the word processor you use to edit your private journal, use libraries written by strangers which may be malicious and have complete access to all of your data.

When you're writing a program, you are likely using a library.  If that library has an exploitable vulnerability in it, then not only will it compromise the library's data, but it will compromise all of your data as well.  In other words, when data is breached, everything in the common virtual address space is exposed.  Consequently, programs are not resilient to data breaches.

So, how can we potentially defend against these vulnerabilities? In 2015, Intel Corp. introduced a new feature called Software Guard Extensions, or SGX.  This feature allows for the creation of private enclaves… regions of memory that, once they are initialized, the operating system can not look into.  SGX also includes features to verify the authenticity and pedigree of data that is loaded into an enclave.

For the last several years, there have been two types of programs that utilize SGX:
1.  Specialized enclave-aware libraries that are written with an Intel Software Development Kit (SDK). 
2.  An application program, all of its libraries, and most of an operating system all running in a single enclave.

I'm proposing a new programming paradigm… one where a program and each of its libraries run in their own enclaves. This is difficult to achieve because we have to modify several disparate pieces of well established software.

1.  Modify the interlibrary parameter passing mechanism of the Application Binary Interface (ABI), which defines how various functions in a library are stored and called in a program.  We are proposing/studying two methods: a fast ABI and a secure ABI. We are interested in studying the "cost" of security in terms of application performance.
2.  Modify the program loader to identify the libraries the program needs and put the program and each library in its own private enclave.
3.  Modify the compiler to implement the new ABI when making inter-library calls (including system calls).
4.  Modify the compiler to store a new class of private data inside the enclave (protecting this data from the operating system and other libraries).
5.  Modify the compiler to accept new "pragmas" to configure the enclave so all of the source code is contained in one file (today's SGX SDKs require several source and configuration files).
6.  Modify the program and library startup code (CRTs) to implement several new features:
    - Dispatch function calls from a common entry point to code inside the enclave 
    - Find other enclaves and securely create shared keys with them 
    - Provide a minimal standard library inside the enclave 
    - Deal with interrupts and exceptions

All of our claims can be satisfied with existing SGX capabilities, but programs will have a few limitations:
1.  Program execution will be slower due to the overhead of switching enclaves
2.  Programs would (at a minimum) need to be recompiled
3.  Programs would need some modification to privatize data
4.  There are known SGX exploits and data leaks, mostly arising from architectural side channels (like Spectre and Meltdown)
5.  We are unsure if we can share physical pages between processes (as is common today)

We believe that if this technology becomes pervasive, then Intel would be motivated to improve the speed, security, and feature set of SGX.  If Intel were to implement a mechanism for securely sharing data between enclaves, then we would be able to satisfy the following security claims for a wide variety of programs, including multi-threaded programs:
1.  Data stored on the stack, heap, and global areas could be protected with a recompilation, rather than modifying the program.
2.  Programs would be free to "share data by choice" rather than share it with the world, as is done today.

We would like to work with Intel to design/propose these changes to SGX.  It's unknown if Intel is considering these changes.


