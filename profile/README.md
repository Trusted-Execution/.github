<img src="https://github.com/Trusted-Execution/.github/blob/main/profile/UHMLogo.png"
     alt="CoE Logo" align="left" height="80" />
<img src="https://github.com/Trusted-Execution/.github/blob/main/profile/CollegeOfEngineering.png"
     alt="CoE Logo" align="right" width="80" />
# Trusted Execution 

Aloha and welcome to the home of the Trusted Execution Lab here at the University of Hawaii's College of Engineering.
Our research is focused on techniques to improve the security of our data and applications in an era of increasing cyber threats.

## Pages

- [Terminology](Terminology.md)



## Notes
- With Skylake-generation CPUs, SGX's Attestation Scheme you had to get a licnese from Intel for each enclave
- Gemini Lake allowed "Flexile Launch Control" where you can sign your own enclaves
- In Feb, 2021, the Linux Kernel mainlained some SGX support into the 5.11 kernel
- 

## Maintainers
- Mail patches to: Jarkko Sakkinen <jarkko@kernel.org>
- Reviewer:        Dave Hansen <dave.hansen@linux.intel.com>
- Mailing list:    linux-sgx@vger.kernel.org
- Status:          Supported
- Files:           Documentation/arch/x86/sgx.rst
- Files:           arch/x86/entry/vdso/vsgx.S
- Files:           arch/x86/include/asm/sgx.h
- Files:           arch/x86/include/uapi/asm/sgx.h
- Files:           arch/x86/kernel/cpu/sgx/*
- Files:           tools/testing/selftests/sgx/*
