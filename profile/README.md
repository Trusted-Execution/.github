<img src="https://github.com/Trusted-Execution/.github/blob/main/profile/UHMLogo.png"
     alt="CoE Logo" align="left" height="80" />
<img src="https://github.com/Trusted-Execution/.github/blob/main/profile/CollegeOfEngineering.png"
     alt="CoE Logo" align="right" width="80" />
# Trusted Execution 

Aloha and welcome to the home of the Trusted Execution Lab here at the University of Hawaii's College of Engineering.
Our research is focused on techniques to improve the security of our data and applications in an era of increasing cyber threats.

## Terminology

Language is important... ABIs, APIs and English are all variations of the same theme:  An agreement amongst producers and consumers on a set of conventions for communicating information.  To that end, there's some terminilogy that we should identify up-front and try to use it consistently throughout this project:

- **Executable**:  A file that contains executable code.  Generally executables can be either a Library or a Main
- **Library**:  An executable that's intended to be shared by several Main files
- **Main**:  An executable with an entry point
- **Static Main**:  An executable that's been statically compiled and needs no Libraries
- **User Process**:  This is an instance of exactly 1 copy of ld, 1 Main and zero or more Libraries.
  -- Within a normal process, executables have no mechanism to keep secrets from each other
  -- Within a normal process, there is no mechanism to that an executable can use to make risk decisions about which Library to bind to it (libraries can have dependencies on other libraries)
  -- Within a normal process, there is no mechanism to ensure that an executable is genuine


## SGX Features this project will use
This stuff you'll have to pay attention to:

- **Architectural Enclaves**:  AEs are “system” enclaves concerned with starting or attesting other enclaves. Intel provides reference implementations of these enclaves, though other companies may write their own.
  -- Provisioning Enclave
  -- Launch Enclave
  -- Quoting Enclave  (we will probably not use)
- **AEX** and **AEX-notify**: Asynchronous Enclave Exit Notify (AEX-Notify) is an architectural extension to
Intel SGX that allows SGX enclaves to be notified after an asynchronous enclave exit (AEX) has occurred. This mechanism can be used by enclave software to react to interrupts and exceptions
- **EPID**: is the attestation protocol originally shipped with SGX. It was replaced by DCAP.  This is intended for client enclaves and deprecated for server environments.
- **SPID**: An identifier one can obtain from Intel, required to make use of EPID attestation.
- **Flexible Launch Control**: FLC is a CPU feature that allows substituting Launch Enclave for one not signed by Intel. A change in SGX’s EINIT logic to not require the EINITTOKEN from the Intel-based Launch Enclave. An MSR, which can be locked at boot time, keeps the hash of the public key of the “launching” entity. With FLC, Launch Enclave can be written by other companies (other than Intel) and must be signed with the key corresponding to the one locked in the MSR (a reference Launch Enclave simply allows all enclaves to run). The MSR can also stay unlocked and then it can be modified at run-time by the VMM or the OS kernel. Support for FLC can be detected using CPUID instruction, as CPUID.07H:ECX.SGX_LC[bit 30] == 1

## SGX Features we may use
**Intel SGX SDK**: In the context of SGX, this means a specific piece of software supplied by Intel which helps people write enclaves packed into .so files to be accessible like normal libraries (at least on Linux). Available together with a kernel module and documentation.

## SGX Features this project will not use
You'll see references to these things in the documentation, but you can safely ignore this stuff for this project.
- **Attestation**:  Attestation is a mechanism to prove the trustworthiness of the SGX enclave to a local or remote party
- **SGX Quote** and **Quoting Enclave**:
- **Data Center Attestation Primitives**: DCAP
- **Intel Attestation Service**: IAS is an Internet service provided by Intel for “old” EPID-based remote attestation.

## Notes
- With Skylake-generation CPUs, SGX's Attestation Scheme you had to get a licnese from Intel for each enclave
- Gemini Lake allowed "Flexile Launch Control" where you can sign your own enclaves
- In Feb, 2021, the Linux Kernel mainlained some SGX support into the 5.11 kernel
