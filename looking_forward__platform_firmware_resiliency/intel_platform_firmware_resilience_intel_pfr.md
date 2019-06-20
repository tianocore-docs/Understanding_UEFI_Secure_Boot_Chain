<!--- @file
  intel-platform-firmware-resilience-intel-pfr.md for Understanding the UEFI Secure Boot Chain

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

## Intel® Platform Firmware Resilience (Intel® PFR) {#intel-platform-firmware-resilience-intel-pfr}

To reduce firmware-related security risks, Intel developed [Intel PFR](https://www.intel.com/content/www/us/en/data-center-blocks/business/firmware-resilience-blocks-solution-brief.html) for server platforms. This feature protects critical firmware from attacks during boot and runtime. It can be treated as an implementation of Project Cerberus or NIST SP800-193.

Intel PFR also enables a protect-in-transit feature, allowing customers to lock and unlock systems to guard against firmware changes during shipment. and “Intel transparent supply chain with platform certificate to create transparency in the supply chain to prevent counterfeit components from being used.”

Figure 4-7 shows the Intel PFR system diagram. Figure 4-8 shows the Intel PFR boot flow. Figure 4-9 shows the Intel PFR reset sequence.

![](/media/image21.png)

###### Figure 4-7: Intel® PFR Overview (source: [csdn.net](https://blog.csdn.net/zdx19880830/article/details/84190005)){#4-7-intel-pfr-overview-source-csdn-net}

![](/media/image22.png)

###### Figure 4-8: Intel® PFR boot flow (source: [csdn.net](https://blog.csdn.net/zdx19880830/article/details/84190005)){#4-8-intel-pfr-boot-flow-source-csdn-net}

![](/media/image23.png)

###### Figure 4-9: Intel® PFR Reset Sequence (source: [csdn.net](https://blog.csdn.net/zdx19880830/article/details/84190005)){#4-9-intel-pfr-reset-sequence-source-csdn-net}