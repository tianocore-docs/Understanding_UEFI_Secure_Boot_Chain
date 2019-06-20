<!--- @file
  Overview.md for Understanding the UEFI Secure Boot Chain
<!--- @file
  Overview.md for Understanding the UEFI Secure Boot Chain

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

## Integrity Models {#integrity-models}

The UEFI Secure Boot chain can be applied to the [Clark-Wilson integrity policy](http://theory.stanford.edu/~ninghui/courses/Fall03/papers/clark_wilson.pdf), developed in 1987\. The Clark Wilson model includes the following concepts:

1.  Data Item:

    1.  Constrained Data Item (CDI)
    2.  Unconstrained Data Item (UDI)

2.  Procedure:

    1.  Integrity Verification Procedure (IVP)
    2.  Transformation Procedures (TPs)

3.  Rule:

    1.  Certification Rule (CR) – integrity monitoring

        1.  **C1**: (Basic: IVP Certification) All IVPs must properly ensure that all CDIs are in a valid state.

        2.  **C2**: (Basic: Validity) All TPs must be certified to be valid. For each TP and each set of CDI that it may manipulate, the security officer must specify a “relation” of the form: (TP, {CDI}).

        3.  **C3**: (Separation of Duty Certification) The list of relation in E2 must be certified to meet the separation of duty requirement.

        4.  **C4**: (Journal Certification) All TPs must be certified to write to an append-only CDI (the log) all information necessary to permit the nature of the operation to be reconstructed.

        5.  **C5**: (Transformation Certification) Any TP that takes a UDI as an input value must be certified to perform only valid transformations, or no transformations, for any possible value of the UDI. The transformation should take the input from a UDI to a CDI, or the UDI is rejected.

    2.  Enforcement Rule (ER) – integrity preserving

        1.  **E1**: (Basic: Enforcement of Validity) The system must maintain the list of relation specified in C2, and must ensure that only TPs certified to run on a CDI manipulate that CDI.

        2.  **E2**: (Enforcement of Separation of Duty) The system must associate a user with each TP and set of CDIs in a list of relations of the form: (User, TP, {CDI}). It must ensure that only executions described in one of the relations are performed.

        3.  **E3**: (User Identity) The system must authenticate the identity of each user attempting to execute a TP.

        4.  **E4**: (Initiation) Only the agent permitted to certify entities may change the list of such entities associated with other entities, specifically the one associated with a TP. An agent that can certify an entity may not have any execute rights concerning that entity.

This model is based on the relationship between authenticated principal, program, and data items. The elements of this relationship are referred to as the “Clark-Wilson Triple” (User, TP, {CDI}). The Clark-Wilson model shows the rules required to meet the security properties of integrity: (from [Blake](https://www.giac.org/paper/gsec/835/clark-wilson-security-model/101747)).

Table 1-1: Clark-Wilson model

| **Property** | **Description** | **Rule** |
| --- | --- | --- |
| **Integrity** | An assurance that CDIs can only be modified in constrained ways to produce valid CDIs. | C1, C2, C5, E1, E4 |
| **Access Control** | The ability to control access to resources. | C3, E2, E3 |
| **Auditing** | The ability to ascertain the changes made to CDIs and ensure that the system is in a valid state. | C1, C4 |
| **Accountability** | The ability to uniquely associate users with their actions. | E3. |

![](media/image1.png)

###### Figure 1-1: Clark-Wilson model, From [Lee](http://www.cl.cam.ac.uk/~mgk25/lee-essays.pdf){#clark-wilson-model-from-lee}

Because the Clark-Wilson focuses on duty and transaction, it is more applicable to business and industry processes. Currently, some papers describe how to apply the Clark-Wilson integrity model to the existing system, such as [Windows](https://www.giac.org/paper/gsec/835/clark-wilson-security-model/101747), [Java](https://docplayer.net/36680206-Supporting-real-world-security-models-in-java.html) or [Trusted Computing Group (TCG) security](https://www.semanticscholar.org/paper/A-Comparison-of-the-trusted-Computing-Group-Model-Smith/fa82426d99b86d1040f80b8bd8e0ac4f785b29a6).

