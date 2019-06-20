<!--- @file
  other-platform-firmware-resiliency-pfr-implementations.md for Understanding the UEFI Secure Boot Chain

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


## Other Platform Firmware Resiliency (PFR) Implementations {#other-platform-firmware-resiliency-pfr-implementations}

Additional PFR solutions are available for implementing NIST SP800-193, such as the [Lattice Root of Trust FPGA solution](http://www.latticesemi.com/pfr) (see Figure 4-12).

![](/media/image26.png)

###### Figure 4-12: Lattice PFR (source: [latticesemi.com/pfr](http://www.latticesemi.com/pfr)).{#4-12-lattice-pfr-source-latticesemi.com-pfr}

The difference in implementations is hardware RoT device selection. Selections include processor microcode, CPLD devices, or FPGA devices. Each has its particular advantages and disadvantages. For example, processor microcode has a limited protection scope, which is why many customers use add-on devices for hardware RoT (CPLD, FPGA).