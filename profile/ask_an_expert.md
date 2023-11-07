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
- Has Intel abandoned their signing process?  What was their thinking around this?  How can trusted computing embrace
  CPU-enfored (low-TCB) attributed code and get away from anonynmous code?
- Does the TCS, specifically, TCS.OENTRY have to be signed?  Is there any way around that?  In other
  words, is there any way to jump to an arbitrary address inside an enclave?
- How can we share data between enclaves by choice?  Can we create an amalgam enclave?
- What's the deak with ME and TX?  Why did Intel drop support fo ME?  It's a powerful feature.  Is there
  a way to enable it?
- Enclave sizes must be a power of 2, do you foresee that as an issue if SGX scales up?
  
### Linux Kernel SGX experts like Jarko
- What are your thoughts on allowing non-privlidged users to create enclaves?  Right now, only privlidged
  users can create an enclave?

### Answers to SGX questions

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
