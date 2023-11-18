# Resources and Learning SGX

## Git Resources
Pull requests let you tell others about changes you've pushed to a branch in a repository on GitHub. 
Once a pull request is opened, you can discuss and review the potential changes with collaborators 
and add follow-up commits before your changes are merged into the base branch.

Use this [template](https://www.freecodecamp.org/news/how-to-make-your-first-pull-request-on-github-3/) 
to make updates to our [SGX-hardware](https://github.com/Trusted-Execution/SGX-hardware) repo:

Initial setup:

    $ git clone https://github.com/Trusted-Execution/SGX-hardware
    $ cd SGX-hardware

Setup for more changes:

    $ git pull origin [Branch Name]

Changing the repo with the intent to do a Pull Request:

    $ git checkout -b [Branch Name]
  
During development & testing:
  
    $ git add .
    $ git commit -m "Your detailed commit message"

When you're ready to push to GitHub:

    $ git push origin [Branch Name]

Navigate to our SGX-hardware repo and initiate a pull request.


## Linux Kernel Resources
- A good place to view and search Linux Kernel source code:  https://elixir.bootlin.com/linux/latest/source

- And the Linux Foundation's reference specs:  https://refspecs.linuxfoundation.org

## Linker Resources
Linkers are really a black box for most programmers.  I bet there's less than 100 people in the world
who have a low-level understaning of linking, yet every-single-program we run has likely been linked.
It's amazing that such a linchpin technology is so little understood.  

- Ian Lance Taylor has a series of articles on linkers:  https://reverseengineering.stackexchange.com/questions/1992/what-is-plt-got

- The book on ld.so:  https://man7.org/linux/man-pages/man8/ld.so.8.html

## Linux 64-bit ABI Resources
- Here's a good guide:  https://www.agner.org/optimize/calling_conventions.pdf
- And the universal reference:  https://en.wikipedia.org/wiki/X86_calling_conventions


## Making calls into shared libraries
- PLT & GOT tutorial:  https://www.technovelty.org/linux/plt-and-got-the-key-to-code-sharing-and-dynamic-libraries.html
- [Understanding _dl_runtime_resolve()](https://ypl.coffee/dl-resolve/)
- [The Procedure Lookup Table](https://bottomupcs.sourceforge.net/csbu/x3882.htm)
- Another article:  https://www.linkedin.com/pulse/elf-linux-executable-plt-got-tables-mohammad-alhyari/

  
## Linux ELF File Format
- ELF Linux Executable PLT and GOT Tables:  https://www.linkedin.com/pulse/elf-linux-executable-plt-got-tables-mohammad-alhyari/
- [man readelf](https://man.archlinux.org/man/readelf.1.en)
- [man objdump](https://man.archlinux.org/man/objdump.1)

## C Language Standard
- The C++ and C programming languages are described here (C is at the bottom): https://en.cppreference.com.  Remember:  These are separate languages!
- How `main()` works:  https://en.cppreference.com/w/c/language/main_function
- A bit more about CRT:  https://en.wikipedia.org/wiki/Crt0

  
## Want to learn about SGX, here's my recommended cirricula:
A good 90-minute video, hosted by one of SGX's designers, describing the technology at a low level:  https://www.youtube.com/watch?v=mPT_vJrlHlg


## Other
- I've always liked Agner Fog's resources, so I'm linking to it:  https://www.agner.org/optimize/

- Changing the entry point of a program:  https://girishjoshi.io/post/changing-entry-point-of-a-c-program/#:~:text=By%20default%20compilers%20(%20gcc%20and,of%20gcc%20can%20be%20used.

- We need to get a little smarter on Intel TDX:
  - https://www.intel.com/content/www/us/en/developer/tools/trust-domain-extensions/overview.html
  - https://arxiv.org/pdf/2303.15540.pdf

