<!--- @file
  References.md for Understanding the UEFI Secure Boot Chain

  Copyright (c) 2019, Intel Corporation. All rights reserved.<BR>

  Redistribution and use in source (original document form) and 'compiled'
  forms (converted to PDF, epub, HTML and other formats) with or without
  modification, are permitted provided that the following conditions are met:

  1) Redistributions of source code (original document form) must retain the
     above copyright notice, this list of conditions and the following
     disclaimer as the first lines of this file unmodified.

  2) Redistributions in compiled form (transformed to other DTDs, converted to
     PDF, epub, HTML and other formats) must reproduce the above copyright
     notice, this list of conditions and the following disclaimer in the
     documentation and/or other materials provided with the distribution.

  THIS DOCUMENTATION IS PROVIDED BY TIANOCORE PROJECT "AS IS" AND ANY EXPRESS OR
  IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF
  MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO
  EVENT SHALL TIANOCORE PROJECT  BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL,
  SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO,
  PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS;
  OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY,
  WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR
  OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS DOCUMENTATION, EVEN IF
  ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

-->
# _References_ {#references}

### Books and Papers {#books-and-papers}

[Amoroso] Amoroso, Edward. Fundamentals of Computer Security Technology. Prentice Hall, 1994

[Bell–LaPadula] Looking Back at the Bell-La Padula Model, 2005, https://www.acsac.org/2005/papers/Bell.pdf

[Biba] Integrity Considerations for Secure Computer Systems, 1975, [http://seclab.cs.ucdavis.edu/projects/history/papers/biba75.pdf](http://seclab.cs.ucdavis.edu/projects/history/papers/biba75.pdf)

[Bishop] Bishop, Matt. Computer Security: Art and Science. Addison-Wesley Professional, 2018

[Blake] Blake, Sonya Q., “The Clark-Wilson Security Model”, SANS Institute Information, May 17, 2000\. [https://www.giac.org/paper/gsec/835/clark-wilson-security-model/101747](https://www.giac.org/paper/gsec/835/clark-wilson-security-model/101747)

[Clark-Wilson] A Comparison of Commercial and Military Computer Security Policies, 1987, [http://theory.stanford.edu/~ninghui/courses/Fall03/papers/clark_wilson.pdf](http://theory.stanford.edu/~ninghui/courses/Fall03/papers/clark_wilson.pdf)

[CW-Lite] Toward Automated Information-Flow Integrity Verification for Security-Critical Applications, [http://www.cse.psu.edu/~trj1/papers/ndss06.pdf](http://www.cse.psu.edu/~trj1/papers/ndss06.pdf), [http://www.cse.psu.edu/~trj1/cse544-s10/slides/Info-Flow-NDSS-2006.pdf](http://www.cse.psu.edu/~trj1/cse544-s10/slides/Info-Flow-NDSS-2006.pdf)

[Lee] Prof. E. Stewart Lee, Director. “Essays about Computer Security.” Centre for Communications Systems Research, Cambridge, 1999\. [http://www.cl.cam.ac.uk/~mgk25/lee-essays.pdf](http://www.cl.cam.ac.uk/~mgk25/lee-essays.pdf)

[NIST SP800-147] BIOS Protection Guidelines, 2011, [https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-147.pdf](https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-147.pdf)

[NIST SP800-147B] BIOS Protection Guidelines for Servers, 2014, [https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-147B.pdf](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-147B.pdf)

[NIST SP800-193] Platform Firmware Resiliency Guidelines, 2018, [https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-193.pdf](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-193.pdf)

[Smith] Ned Smith, A Comparison of the trusted Computing Group Security Model with Clark-Wilson, 2014, [https://www.semanticscholar.org/paper/A-Comparison-of-the-trusted-Computing-Group-Model-Smith/fa82426d99b86d1040f80b8bd8e0ac4f785b29a6](https://www.semanticscholar.org/paper/A-Comparison-of-the-trusted-Computing-Group-Model-Smith/fa82426d99b86d1040f80b8bd8e0ac4f785b29a6)

[Welch] Welch, Ian and Stroud, Robert. Supporting Real World Security Models in Java, 7<sup>th</sup> IEEE Workshop on Future Trends of Distributed Computing Systems, FTDCS&#039;99\. Cape Town, South Africa, December 20-22, 1999.

### Web {#web}

[AndroidVerifiedBoot] Android Verified Boot, [https://source.android.com/security/verifiedboot](https://source.android.com/security/verifiedboot)

[AndroidVerifiedBoot2] Android Verified Boot 2.0, [https://android.googlesource.com/platform/external/avb/+/master/README.md](https://android.googlesource.com/platform/external/avb/+/master/README.md)

[AndroidVerifiedBoot3] Android Verified Boot 2.0, [https://blog.csdn.net/rikeyone/article/details/80606147](https://blog.csdn.net/rikeyone/article/details/80606147)

[BootGuard] Direct from Development – Cyber Resiliency In Chipset and BIOS, [https://downloads.dell.com/solutions/servers-solution-resources/Direct%20from%20Development%20-%20Cyber-Resiliency%20In%20Chipset%20and%20BIOS.pdf](https://downloads.dell.com/solutions/servers-solution-resources/Direct%20from%20Development%20-%20Cyber-Resiliency%20In%20Chipset%20and%20BIOS.pdf)

[CapsuleRecovery] Jiewen Yao, Vincent Zimmer, A Tour Beyond BIOS- Capsule Update and Recovery in EDK II, https://github.com/tianocore-docs/Docs/raw/master/White_Papers/A_Tour_Beyond_BIOS_Capsule_Update_and_Recovery_in_EDK_II.pdf

[Cerberus] Project Cerberus Architecture Overview, etc, [https://github.com/opencomputeproject/Project_Olympus/blob/master/Project_Cerberus](https://github.com/opencomputeproject/Project_Olympus/blob/master/Project_Cerberus/Project%20Cerberus%20Architecture%20Overview.pdf)

[Cerberus2] Bryan Kelly, Project Cerberus Hardware Security, 2018,

[https://f990335bdbb4aebc3131-b23f11c2c6da826ceb51b46551bfafdc.ssl.cf2.rackcdn.com/images/fbbdd5feceb6e6328373417e1ab7c06a13a2ef2c.pdf](https://f990335bdbb4aebc3131-b23f11c2c6da826ceb51b46551bfafdc.ssl.cf2.rackcdn.com/images/fbbdd5feceb6e6328373417e1ab7c06a13a2ef2c.pdf)

[CorebootVerifiedBoot] vboot – Verified Boot Support, [https://doc.coreboot.org/security/vboot/index.html?highlight=verified%20boot](https://doc.coreboot.org/security/vboot/index.html?highlight=verified%20boot)

[CorebootVerifiedBoot2] Simon Glass, Verified boot in Chrome OS and how to make it work for you, [https://static.googleusercontent.com/media/research.google.com/en//pubs/archive/42038.pdf](https://static.googleusercontent.com/media/research.google.com/en/pubs/archive/42038.pdf)

[CorebootVerifiedBoot3] Randall Spangler, Verified boot surviving in the internet of insecure things, [https://www.coreboot.org/images/c/ce/Verified_Boot_-_Surviving_in_the_Internet_of_Insecure_Things.pdf](https://www.coreboot.org/images/c/ce/Verified_Boot_-_Surviving_in_the_Internet_of_Insecure_Things.pdf)

[DICE] TCG DICE, [https://trustedcomputinggroup.org/work-groups/dice-architectures/](https://trustedcomputinggroup.org/work-groups/dice-architectures/)

[FirmwareSecurity] Dell Firmware Security, [https://www.platformsecuritysummit.com/2018/speaker/johnson/PSEC2018-Dell-Firmware-Security-Justin-Johnson.pdf](https://www.platformsecuritysummit.com/2018/speaker/johnson/PSEC2018-Dell-Firmware-Security-Justin-Johnson.pdf)

[GoogleTitan] Titan in depth security in plaintext, [https://cloud.google.com/blog/products/gcp/titan-in-depth-security-in-plaintext](https://cloud.google.com/blog/products/gcp/titan-in-depth-security-in-plaintext)

[GoogleTitan2] Scott Johnson, [https://keystone-enclave.org/workshop-website-2018/slides/Scott_Google_Titan.pdf](https://keystone-enclave.org/workshop-website-2018/slides/Scott_Google_Titan.pdf)

[HIRS] Host Integrity at Runtime and Startup [https://github.com/nsacyber/hirs](https://github.com/nsacyber/hirs)

[Intel Security] security-technologies-4th-gen-core, https://www.intel.com/content/dam/www/public/us/en/documents/white-papers/security-technologies-4th-gen-core-retail-paper.pdf 

[IntelPFR] PFR server blocks solution, [https://www.intel.com/content/dam/www/public/us/en/documents/solution-briefs/pfr-server-blocks-solution-brief.pdf](https://www.intel.com/content/dam/www/public/us/en/documents/solution-briefs/pfr-server-blocks-solution-brief.pdf)

[IntelPFR2] Intel Platform Firmware Resilience, [https://blog.csdn.net/zdx19880830/article/details/84190005](https://blog.csdn.net/zdx19880830/article/details/84190005)

[LatticePFR] Universal Platform Firmware Resilience solution, [http://www.latticesemi.com/zh-CN/Solutions/Solutions/SolutionsDetails02/PFR](http://www.latticesemi.com/zh-CN/Solutions/Solutions/SolutionsDetails02/PFR)

[Linux MOK] Ubuntu Secure Boot, [https://wiki.ubuntu.com/UEFI/SecureBoot](https://wiki.ubuntu.com/UEFI/SecureBoot)

[Linux MOK2] Olaf Kirch, UEFI Secure Boot, [https://www.suse.com/media/presentation/uefi_secure_boot_webinar.pdf](https://www.suse.com/media/presentation/uefi_secure_boot_webinar.pdf)

[PCIeAuth] PCIe* Component Authentication

[https://pcisig.com/pcie%C2%AE-component-authentication](https://pcisig.com/pcie%C2%AE-component-authentication)

[PCIeSecurity] PCIe* Device Security Enhancements Specification, [https://www.intel.com/content/www/us/en/io/pci-express/pcie-device-security-enhancements-spec.html](https://www.intel.com/content/www/us/en/io/pci-express/pcie-device-security-enhancements-spec.html)

[S3Resume] Jiewen Yao, Vincent Zimmer, [A Tour Beyond BIOS Implementing S3 Resume with EDK II](https://github.com/tianocore-docs/Docs/raw/master/White_Papers/A_Tour_Beyond_BIOS_Implementing_S3_resume_with_EDKII_V2.pdf), [https://github.com/tianocore-docs/Docs/raw/master/White_Papers/A_Tour_Beyond_BIOS_Implementing_S3_resume_with_EDKII_V2.pdf](https://github.com/tianocore-docs/Docs/raw/master/White_Papers/A_Tour_Beyond_BIOS_Implementing_S3_resume_with_EDKII_V2.pdf)

[SECURE1] Jacobs, Zimmer, &quot;Open Platforms and the impacts of security technologies, initiatives, and deployment practices,&quot; Intel/Cisco whitepaper, December 2012, [http://uefidk.intel.com/sites/default/files/resources/Platform_Security_Review_Intel_Cisco_White_Paper.pdf](http://uefidk.intel.com/sites/default/files/resources/Platform_Security_Review_Intel_Cisco_White_Paper.pdf)

[SECURE2] Magnus Nystrom, Martin Nicholes, Vincent Zimmer, &quot;UEFI Networking and Pre-OS Security,&quot; in Intel Technology Journal - UEFI Today:  Boostrapping the Continuum, Volume 15, Issue 1, pp. 80-101, October 2011, ISBN 978-1-934053-43-0, ISSN 1535-864X

[https://www.researchgate.net/publication/235258577_UEFI_Networking_and_Pre-OS_Security/file/9fcfd510b3ff7138f4.pdf](https://www.researchgate.net/publication/235258577_UEFI_Networking_and_Pre-OS_Security/file/9fcfd510b3ff7138f4.pdf) 

[SECURE3] Zimmer, Shiva Dasari (IBM), Sean Brogan (IBM), “Trusted Platforms:  UEFI, PI, and TCG-based firmware,” Intel/IBM whitepaper, September 2009, [http://www.cs.berkeley.edu/~kubitron/courses/cs194-24-S14/hand-outs/SF09_EFIS001_UEFI_PI_TCG_White_Paper.pdf](http://www.cs.berkeley.edu/~kubitron/courses/cs194-24-S14/hand-outs/SF09_EFIS001_UEFI_PI_TCG_White_Paper.pdf)

[SmmComm] Jiewen Yao, Vincent Zimmer, Star Zeng, A Tour Beyond BIOS Secure SMM Communication, [https://github.com/tianocore-docs/Docs/raw/master/White_Papers/A_Tour_Beyond_BIOS_Secure_SMM_Communication.pdf](https://github.com/tianocore-docs/Docs/raw/master/White_Papers/A_Tour_Beyond_BIOS_Secure_SMM_Communication.pdf)

[SPDM] Security Protocol and Data Model Specification, [https://www.dmtf.org/sites/default/files/standards/documents/DSP0274_0.9.0a.pdf](https://www.dmtf.org/sites/default/files/standards/documents/DSP0274_0.9.0a.pdf)

[SPDMonMCTP] SPDM over MCTP Binding Specification, [https://www.dmtf.org/sites/default/files/standards/documents/DSP0275_0.9.0a.pdf](https://www.dmtf.org/sites/default/files/standards/documents/DSP0275_0.9.0a.pdf)

[TXT] Intel TXT software development guide, [https://www.intel.com/content/dam/www/public/us/en/documents/guides/intel-txt-software-development-guide.pdf](https://www.intel.com/content/dam/www/public/us/en/documents/guides/intel-txt-software-development-guide.pdf)

[UEFI] Unified Extensible Firmware Interface (UEFI) Specification, Version 2.5

[www.uefi.org](http://www.uefi.org)

[UEFI Book] Zimmer, et al, “Beyond BIOS: Developing with the Unified Extensible Firmware Interface,” 2<sup>nd</sup> edition, Intel Press, January 2011

[UEFI Overview] Zimmer, Rothman, Hale, “UEFI: From Reset Vector to Operating System,” Chapter 3 of _Hardware-Dependent Software_, Springer, February 2009

[UEFI PI Specification] UEFI Platform Initialization (PI) Specifications, volumes 1-5, Version 1.3 [www.uefi.org](http://www.uefi.org)

[USBAuth] Universal Serial Bus Type-C™ Authentication Specification, [https://www.usb.org/document-library/usb-authentication-specification-rev-10-ecn-and-errata-through-january-7-2019](https://www.usb.org/document-library/usb-authentication-specification-rev-10-ecn-and-errata-through-january-7-2019)

[Variable] Jiewen Yao, Vincent Zimmer, Star Zeng, A Tour Beyond BIOS Implementing UEFI Authenticated Variables in SMM with EDK II, [https://github.com/tianocore-docs/Docs/raw/master/White_Papers/A_Tour_Beyond_BIOS_Implementing_UEFI_Authenticated_Variables_in_SMM_with_EDKII_V2.pdf](https://github.com/tianocore-docs/Docs/raw/master/White_Papers/A_Tour_Beyond_BIOS_Implementing_UEFI_Authenticated_Variables_in_SMM_with_EDKII_V2.pdf)