<img src="https://github.com/Trusted-Execution/.github/blob/main/profile/UHMLogo.png"
     alt="CoE Logo" align="left" height="80" />
<img src="https://github.com/Trusted-Execution/.github/blob/main/profile/CollegeOfEngineering.png"
     alt="CoE Logo" align="right" width="80" />
# Notes on SGX in the Linux Kernel 

## Notes
- In Feb, 2021, the Linux Kernel mainlained some SGX support into the 5.11 kernel

## Linux Kernel Codebase and Maintainers
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
