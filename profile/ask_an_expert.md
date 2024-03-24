<img src="https://github.com/Trusted-Execution/.github/blob/main/profile/UHMLogo.png"
     alt="CoE Logo" align="left" height="80" />
<img src="https://github.com/Trusted-Execution/.github/blob/main/profile/CollegeOfEngineering.png"
     alt="CoE Logo" align="right" width="80" />
# Ask an Expert

So many times in my career have I wanted to sit with an expert in subject X and just talk with them.
That's the hard part about being a senior engineer; oftentimes, the pool of people you can lean on for
technical issues gets smaller and smaller.  The trick, of course, is to develop a network of experts,
oftentimes outside of your organization, who you can reach out to.

There are very few people who have deep, hands-on expertise in SGX.  For this project, we will
be digging into more than just SGX, we'll be into compilers, loaders and maybe even the Linux kernel
itself.

This page is intended to be a place where we can document the questions we'd like to ask an expert.
I've found that sometimes, just the act of clearly articulating the question in writing often yields
some insight into the problem.

Over the course of this project, if we get cornered and we need to reach out and find an expert, then
that's what we will do.  To that end, I'd like a central place where we can document the questions
we'd like to ask.

## SGX
### General SGX Questions

### Intel
- How can we talk to your SGX team?
- What is Intel's roadmap for SGX?
- Has Intel abandoned their signing process?
  - What was their thinking around this?
  - How can trusted computing embrace CPU-enfored (low-TCB) attributed code and get away from anonynmous code?
- How can we share data between enclaves by choice?  Can we create an amalgam enclave?
- What's the deal with ME and TX?  Why did Intel drop support fo ME?  It's a powerful feature.  Is there
  a way to enable it?
- Enclave sizes must be a power of 2, do you foresee that as an issue if SGX scales up?
- Establishing a Commercial Agreement:
  -- How hard is it to establish a Commercial Agreement?
  -- Can academics do it?
  -- Can an ordinary developer do it?  Would Intel be interested in scaling this up to "App Store" levels?
  -- What are our options for storing/managing a signing key?  What are some examples of things that Intel has allowed?
  -- What are some examples of things Intel has said "No" to?

#### Intel Feature Requests
  - The ability for one enclave to directly call another enclave.  This would eliminate a lot of CRT code.
    - Just EENTER... that's all.  Not EINIT, EADD, et. al..
  - I think CET should be mantadory.  I know this won't be popular, but the ability to return to
    arbitrary code in SGX eliminates a lot of the saftey nets.  Use case:  Put a call stack outside
    the enclave and see what happens.
    - You could also consider modifying RET to verify that the stack is inside an enclave (but that would break my code).
  - Multiple stacks.  I'd love to be able to use other registers to manage a private in-enclave stack alongside the public stack.  CET already has the concept of a shadow stack... take it to the next level.
  - Sharing data between multiple enclaves.  I know this is hard... but it can be done.
  - Larger EPCs.  Can we find a way to dynamically add/remove EPC, so some machines can be no-SGX and others can be all-SGX?  The current setup is untennable.
  - I really love the Memory Encryption Engine.  What can we do to get that back?
  - I'd like you to get in the "app store" business... with enclaves.
  - Possible bug:  Let's say we set aside 4K for the SSA.  CPUID tells us that it wants 1088 bytes for XSAVE.  
    Now, set NSSA to a big number (like 14)... the enclave starts and thinks everything is fine even if there's 
    nowhere near that much room in the SSA.
  - My ideal Intel CPU (desktop, enterprise & cloud):  SGX3, AES, SHA, CET, AVX, APX.  No -16 or -32 bit instructions.  No segment registers.  Reclaim your instruction set!  SGX_LC is mandatory if it's a production system.

#### Answers to Intel/SGX questions
  - Question:  Is the TCS signed?  Specifically, is the TCS.OENTRY (Offset in enclave to which control is
    transferred on EENTER relative to the base of the enclave.) signed?
  -- Answer:  The TCS is definately signed.  Intel specifically designed SGX enclaves to have controlled
     entry points to prevent ROP attacks.

  - Question:  Can an SGX enclave span multiple virtual addresses spaces?
  -- Answer:  No, the virtual address base is set when the enclave is created.  There is
     no mechanism for different page-level virtual address bases

  - Question:  How can we tell how large an SSA frame will be?  We know how big the XSAVE area will be.  We know GPRSGX is a fixed size.
  -- Answer:  Use the CPUID instruction. 


### Linux Kernel SGX experts like Jarko
- What are your thoughts on allowing non-privlidged users to create enclaves?  Right now, only privlidged
  users can create an enclave?
- What are the plans for the vDSO?  The documentation says the vDSO function (vdso_sgx_enter_enclave) intercepts
  exceptions that would otherwise generate a signal and return the fault information directly to its caller. This
  avoids the need to juggle signal handlers. I'm not seeing the code that does that.  Am I missing something?  Is
  this planned behavior?
- Are there plans for any more vDSO-based SGX functions?
- I noticed that in line 567 of v6.6.2 of /arch/x86/kernel/cpu/sgx/ioctl.c, the code throws away the return value
  EINIT which would have some valuable debugging data.  The only way to see it is to enable debugging in
  the kernel, and even then, the program wouldn't be able to use it.  Is there a way we can get that error
  number to the calling program?

## Compiler

## Linker

## `glibc` & `ld`
The program header lists the SEGMENT.
- SEGMENTS don't really have names and contain information necessary to load and execute a file.
- SECTIONS have names like `.text`, `.data`, and hold important data for linking and relocation.
- A SEGMENT contains 0 or more SECTIONS.

I've spent a lot of time studying sections (`.text`) but not a lot of time worrying about segments.
`sgx_hello`, however, works at the segment layer (which makes sense as that is loader territory).

So, the question is... How much SGX/TX information do we put in the SEGMENT table?  How do we identify
enclaves, which bits to measure, special SGX regions like the heap (a calloc'd /.bss page) and the
TCB.

Another question:  Does a modern loader look at sections or use section-level information when
it's loading or do modern loaders exclusivley use segments?  Should we even consider breaking
the convention?

- What functions (if any) should be included in a mini-libc inside of each enclave?
-- Pro: these are relatively small and would prevent a lot of inter-enclave thrashing.
-- Pro: can access data inside an enclave (so there may be a minimum we need just to do business)
-- Enclaves must have an internal library at a minimum for some of the enclave maintenance functions in SGX2
## The Linux ABI

## ELF File Formats
Here's a conndrum... Consider backward compatability and situations when a user does not have access to a system with SGX.  Do we build a Universal executable that can run on either platform or do we prevent the executable from running?
  - Pros for Universal:
    -- Usability
  - Cons for Universal:
    -- The app has to tell the user when it's in "Secure Mode" or not
    -- We will be modifying the C programming language... so it really can't (easily) go backwards

I'm thinking of designating a new executable suffix:  `.tx` For Trusted Executable.  I was going to call it `.sgx` but, it's trademarked by Intel and it's a specific implementation.  I'd like any enclave/trusted execution envornment to be able to use this, so let's make it generic.

## Your Deity
- In reimagining (trusted) computing, how can we abstractly adopt non-anonymized code?  We need a
  positive name for this concept.  For this to be low TCB, we need it in the UEFI/BIOS simliar to how we set
  virtual mode, sgx mode, etc. Setting the flags in real mode before switching modes and then booting the
  OS.  What would this be?  A binary switch:  PRODUCTION / DEVELOPMENT (this seems too limiting
  and not very abstract).  How would you abstract this convept?  Right now, I can only think of 2 modes:
  MY_DADS_COMPUTER / IM_A_ROCKSTAR_DEVELOPER but I'm not being very creative.
