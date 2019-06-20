<!--- @file
  google-titan.md for Understanding the UEFI Secure Boot Chain

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

## Google Titan {#google-titan}

Google developed [Titan](https://cloud.google.com/blog/products/gcp/titan-in-depth-security-in-plaintext) as a hardware root-of-trust solution for [Google Cloud Platform](https://cloud.google.com/) (GCP). Aside from basic secure boot, Titan implements remediation and first-instruction integrity. These features are like functions found in Intel Boot Guard and Project Cerberus.

_“Trust can be re-established through remediation in the event that bugs in Titan firmware are found and patched, and first-instruction integrity allows the platform to identify the earliest code that runs on each machine’s startup cycle.”_

_-- “[Titan in depth: Security in plaintext](https://cloud.google.com/blog/products/gcp/titan-in-depth-security-in-plaintext)” (cloud.google.com)_

Figure 4-10 shows the Titan System Integration diagram. Figure 4-11 shows the Titan Verified Boot flow.

![](/media/image24.png)

###### Figure 4-10: Titan System Integration (source: “[Titan silicon root of trust for Google Cloud](https://keystone-enclave.org/workshop-website-2018/slides/Scott_Google_Titan.pdf)”){#4-10-titan-system-integration}

![](/media/image25.png)

###### Figure 4-11: Titan Verified Boot(source: “[Titan silicon root of trust for Google Cloud](https://keystone-enclave.org/workshop-website-2018/slides/Scott_Google_Titan.pdf)”){#4-11-titan-verified-boot}
