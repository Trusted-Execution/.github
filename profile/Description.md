The Project Description
=======================

Today, almost all computer programs are not 100% self-sufficient.  They depend on libraries of code, written by other people, to do their work.  When a computer program is written, the compiler, linker and loader work together to resolve the dependencies needed by the program that is nested within each library.  Later, when the program is run, a loading program finds the library files and "lazily binds" the libraries to the running program.  All of this happens in a common area of memory for the process called a "virtual address space".  Once a library joins this common virtual address space, it can access all of the memory in it.  There is no way for a program to keep a secret from a library.  Furthermore, there is no way for a program, running in this common virtual address space, to keep secrets from the computer’s components such as the operating system, hypervisor, or System Management Module.

In addition to this, most programs never have the opportunity to make decisions about which libraries are bound to it.  They can't tell if they come from trustworthy sources or if they have been tampered with.  Programs that you run today, like your browser or the word processor used to edit your private journal, use libraries written by strangers which may be malicious and have complete access to all of your data.

When you're writing a program, you are likely using a library.  If that library has an exploitable vulnerability in it, then not only will it compromise the library's data, but it will compromise all of your data as well.  In other words, when data is breached, everything in the common virtual address space is exposed.  Consequently, programs are not resilient to data breaches.

So, how can we potentially defend against these vulnerabilities? In 2015, Intel Corp. introduced a new feature called Software Guard Extensions (SGX).  This feature allows for the creation of private enclaves… regions of memory that, once they are initialized, the operating system can not look into.  SGX also includes features to verify the authenticity and providence of data loaded into an enclave.

For the last several years, there have been two types of programs that utilize SGX:
1.  Specialized enclave-aware libraries written with an Intel Software Development Kit (SDK).
2.  An application program, all of its libraries, and most of an operating system all running in a single enclave.

I'm proposing a novel programming paradigm… one where a program and each of its libraries run in their own enclaves. This is difficult to achieve because we have to modify several disparate pieces of well established software. Our novel system includes:

1.  Modify the interlibrary parameter passing mechanism of the Application Binary Interface (ABI), which defines how various functions in a library are stored and called in a program.  We are proposing/studying two novel methods: A fast-mode and a secure-mode ABI. As a matter of academic interest, we intend to study the "cost" of security in terms of application performance.
1.1.  The new ABI would compile the source code of each function into multiple functions:
1.1.1. Function1:  Compile using the existing ABI for backwards compatability
    1.1.2  Function2:  Compile using a "fast-mode" ABI where function requests pass unencrypted parameters via registers and/or the stack.  Function requests, however, flow out of one enclave, through a “double dispatcher” and into a library in its own enclave
    1.2.3  Function 3:  Compile a "secure-mode" ABI where a function request is encrypted via a "secure note" and routed out of one enclave, through a "double dispatcher" and into a library in its own enclave

4.  Modify the program loader, which prepares a program for usage, to identify the libraries the program needs and put the program and each library in its own private enclave.
5.  Modify the compiler, which translates a program into something your computer can understand, to implement a new ABI when making inter-library calls (including system calls).  Use the existing ABI for intra-library calls.
6.  Modify the compiler to store a new class of private data inside the enclave (protecting this data from the operating system and other libraries).
   - This may include secure local variables stored on a stack (the novelty is we will introduce a new storage class to the C programming language)
   - It may include secure global varaibles available to any function or thread within an enclave (the novelty is we will introduce a new storage class to the C programming language)
   - It may include dynamic data stored within an enclave (the enclave must implement its own "malloc" library)
8.  Modify the compiler to accept new "pragmas" (notes/instructions to the complier) to configure the enclave so all of the source code is contained in one file (today's SGX SDKs require several source and configuration files).
9.  Modify the program and library startup code (CRTs) to implement several new features:
    - Dispatch function calls from a common entry point to code inside the enclave. 
    - Find other enclaves and securely create shared keys with them. 
    - Provide a minimal standard library inside the enclave. 
    - Deal with interrupts and exceptions.

All of our claims can be satisfied with existing SGX capabilities, but programs will have a few limitations:
1.  Program execution will be slower due to the overhead of switching enclaves.
2.  Programs would (at a minimum) need to be recompiled.
3.  Programs would need some modification to privatize data.
4.  There are known SGX exploits and data leaks, mostly arising from architectural side channels (like Spectre and Meltdown).
5.  We are unsure if we can share physical pages between processes (as is common today).

We believe that if this technology becomes pervasive, then Intel would be motivated to improve the speed, security, and feature set of SGX.  If Intel were to implement a mechanism for securely sharing data between enclaves, then we would be able to satisfy the following security claims for a wide variety of programs, including multi-threaded programs:
1.  Data stored on the stack, heap, and global areas could be protected with a recompilation, rather than modifying the program.
2.  Programs would be free to "share data by choice" rather than share it with the world, as is done today.

We would like to work with Intel to design/propose these changes to SGX.  It's unknown if Intel is considering these changes.


