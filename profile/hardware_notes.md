<img src="https://github.com/Trusted-Execution/.github/blob/main/profile/UHMLogo.png"
     alt="CoE Logo" align="left" height="80" />
<img src="https://github.com/Trusted-Execution/.github/blob/main/profile/CollegeOfEngineering.png"
     alt="CoE Logo" align="right" width="80" />
# SGX Hardware (and Deprication) Notes

These are unorganized notes that are not ready to publish on the 
[SGX_Hardware](https://github.com/marknelsonengineer/SGX-hardware) site

- With Skylake-generation CPUs, SGX's Attestation Scheme you had to get a licnese from Intel for each enclave
- Gemini Lake allowed "Flexile Launch Control" where you can sign your own enclaves

In addition to the CPU being SGX capable, ARC adds the following reqirements:
- Yes with Intel® SPS - Server Platform Services Management Engine
- Yes with Intel® ME - [Management Engine](https://en.wikipedia.org/wiki/Intel_Management_Engine)

SGX is not in Intel's 13/14 Gen CPUs
Nor is listed in the 12 Gen CPU
It is NOT in the 11th Gen CPU
It IS in the 10th Gen CPU

"Intel deprecated SGX from its 11th and 12th Gen desktop processors"

"continue choosing the 7th - 10th generation of Intel CPUs and motherboards that remain the Intel SGX feature."

https://en.wikipedia.org/wiki/List_of_Intel_CPU_microarchitectures

"Intel continues supporting SGX on their latest Xeon processors but on the client side have been deprecated since 11th Gen Core."

A modern Xeon CPU like the 6444Y 
https://www.intel.com/content/www/us/en/products/sku/232385/intel-xeon-gold-6444y-processor-45m-cache-3-60-ghz/specifications.html
https://ark.intel.com/content/www/us/en/ark/products/232385/intel-xeon-gold-6444y-processor-45m-cache-3-60-ghz.html
https://en.wikipedia.org/wiki/Sapphire_Rapids#Products 
...supports SGX

Intel® Processors Supporting Intel® SGX:
https://www.intel.com/content/www/us/en/architecture-and-technology/software-guard-extensions-processors.html

Intel® Xeon® Scalable Processors
Multi-socket systems containing CPUs of this family support up to 1TB of Enclave Page Cache (EPC)
Ranging from 8G to 512G (Per CPU)

Intel® Xeon® D Processors
- optimized performance in space and power constrained environments (SoC) 
- support up to 64GB of Enclave Page Cache (EPC)

Intel® Xeon® E Processors
- essential, business-ready performance, expandability, and reliability for entry server solutions
- Enclave Page Cache (EPC) varies on these CPUs, but peaks at 512MB (0.5GB)
