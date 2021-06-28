# OpenHW Project Concept Proposal: Hardware Abstraction Layer (HAL)
_The PC proposal introduces the project and explains the market drivers and the "why"_
# Title of Project - "CORE-V HAL"
# Project Concept Proposal
## Date of proposal - 2021-06-28
## Author(s) - Vincent Cui (Alibaba)
## High Level Summary of project, project components, and deliverables
The Hardware Abstract Layer (HAL) project for Core-V-MCU aims to define and release a set of specifications for the OpenHW. It's a software API framework on CORE-V based processors
.It mainly provides unified, consistent access for the operating system layer to the hardware resources of CORE-V cores, CORE-V based chips. It will provide a standard to describe the resources in the chip. 

It also will provide a reference implementation of the specified HAL which will comprise a part of the Core-V-MCU Software Development Kit (SDK), which involves HAL driver of such peripherals Core-V-MCU supports.
By defining a HAL specification applicable to Core-V based hardwares, we can benefit from the HAL-based SDK as follows:

- Offer a common approach to development of driver-level software for Core-V in order to simplify software reuse and reduce cost;
- Make consistent system startup code for system initialization and software access to chip and board level peripherals;
- Enable software developers to develop hardware independent application code as well as firmware developers to communicate with new and customized hardware components under a consistent framework;
- Allows end-users to tailor and extend the HAL to address their own platform requirements according to well defined procedures.
## Summary of market or input requirements
### Known market/project requirements at PC gate

- Significantly reduce cost in SoC driver development, by defining an approach to enable driver reuse according to an accepted framework;
- Make consistent the upper layer software across different SoC. This requires standard HAL APIs to isolate hardware and software resources in such a manner that makes it easy to migrate software across platforms.


| Category     	  		| Req #		| Requirement                  |
|----------	  		|------		|-----------------------------	|
| *Technical Reqmtns*	| T-1     	|HAL MUST support API for core features | 
| 			  	| T-2     	|HAL MUST support API for on-chip peripheral features | 
| 			  	| T-3     	|HAL MUST support both RTOS and bare-metal scenarios |
| 			  	| T-4     	|HAL MUST be able to support bare metal libc |
| 			  	| T-5     	|HAL MUST be able to be extended to support all CORE-V cores for the purpose of RTOS (not Linux) support |
| 			  	| T-6     	|HAL MUST support a description of the chip using a standardized syntax |
| 			  	| T-7     	|HAL SHOULD define a configuration file that can indicate to the IDE low level chip parameters such as memory space and allow it to display/read/write the registers of peripherals |
| 			  	| T-8     	|HAL MAY be able to be extended to support the CORE-V X Coprocessor Interface (CV-X-IF) |
| 			  	| T-9     	|HAL MAY be able to be extended to support the CV-VEC coprocessor | 
| *Industry Adoption Rqmtns*	| IA-1     	|HAL SHOULD be adopted/implemented for other RISC-V devices | 	
| *Specification Rqmtns*	| S-1     	|HAL Specification License for CORE-V MUST be open-source or freely licensed | 			  	| T-2     		| 
| 				| S-2     	|Proprietary extensions to the HAL Specification and Implementation, such as for custom ISA extensions or proprietary chip, MUST be supportable/allowable under open-source license|
| 				| S-3     	|HAL Specification, user documentation, and system implementation documentation for CORE-V HAL MUST be available in English |
| 				| S-4     	|HAL Specification MUST be published and managed by an industry open source or standards body, such as OpenHW, RISC-V International, or FOSSi |
| *Implementation Rqmtns* 	| IM-1     	|A complete open source reference implementation of the HAL for CORE-V MUST be a project deliverable |
| 				| IM-2     	|FreeRTOS SHOULD be supported in the open source reference implementation of HAL for CORE-V |
| 				| IM-3     	|Newlib SHOULD be supported in the open source reference implementation  of HAL for CORE-V |
| 				| IM-3     	|The HAL reference implementation for CORE-V SHOULD be published by the body publishing the Specification (see above) |

### Potential future design enhancements

- Support new peripherals or other Hardware components.
- Create and provide reference designs on application areas such as Neural Network, DSP, Debug & Trace and Security.
## Who would make use of OpenHW output
CORE-V HAL will be used by firmware, middleware and application developers who are developing code supporting Core-V based hardware designs.
It will be a key component of a Core-V MCU SDK.
## Initial Estimate of Timeline
HAL's take many years to develop. Arm CMSIS is around 15 years old. At this stage we propose a 3-month period to agree the approach and develop detailed plans for project launch. At that time we shall have a more accurate understanding of the deliverables and the timescale over which they can be completed.

- To agree the key technical requirements, approach, and specification for a Core-V HAL that will be re-used for all Core-V Cores

Once the HAL approach is agreed

- To implement basic peripherals (UART, TIME, INT...) on Core-V MCU.
- To have FreeRTOS run on Core-V MCU in conjunction with HAL .
- To implement support other peripherals and meet application requirement.
## Explanation of why OpenHW should do this project

- The HAL is needed to establish a baseline approach for addressing the Core-V Cores and peripherals under a consistent approach. It is a cornerstone of all Core-V SDK and software work.
- There are some challenges for Core-V MCU users to develop application bases on adopted PULP SDK due to the complexity of the development configuration environment. The PULP SDK is not viewed as a basis for future development work.
- There should be an out-of-box SDK solution offered by OpenHW supporting Core-V MCU platform developer.
- An easy-to-use SDK enhances the Core-V MCU development environment by reducing the barrier on software development and enabling to create reusable application code.
- There are some requirement from system tools (such as compiler) to help verify their design's performance and correctness using HAL SDK.
## Industry landscape: description of competing, alternative, or related efforts in the industry
There are also some similar standards in market currently, the most representative HAL is below:

1. CMSIS: [https://www.arm.com/why-arm/technologies/cmsis](https://www.arm.com/why-arm/technologies/cmsis)
1. NMSIS: [https://doc.nucleisys.com/nmsis/](https://doc.nucleisys.com/nmsis/)
1. CSI: English version is in preparation： [https://yoc.docs.t-head.cn/yocbook/Chapter3-AliOS/](https://yoc.docs.t-head.cn/yocbook/Chapter3-AliOS/)
1. FreeRTOS CommonIO specification [https://developer.amazon.com/acs-devices](https://developer.amazon.com/acs-devices)

### Table showing how existing solutions map against requirements at Project Concept gate

| Category     	  		| Req #		| CMSIS | NMSIS | CSI | Requirement descriptions                 |
|----------	  		    |------		| ----- | ----- |---- | ------------------------	|
| *Technical Reqmtns*	| T-1     	|  N    | Y     | Y   |HAL MUST support API for core features | 
| 			  	        | T-2     	|  Y    | N     | Y   |HAL MUST support API for on-chip peripheral features | 
| 			  	        | T-3     	|  Y    | Y     | Y   |HAL MUST support both RTOS and bare-metal scenarios |
| 			  	        | T-4     	|  Y    | Y     | Y   |HAL MUST be able to support bare metal libc |
| 			  	        | T-5     	|  Y    | Y     | Y   |HAL MUST be able to be extended to support all CORE-V cores for the purpose of RTOS (not Linux) support |
| 			  	        | T-6     	|  Y    | N     | N   |HAL MUST support a description of the chip using a standardized syntax |
| 			  	        | T-7     	|  Y    | N     | N   |HAL SHOULD define a configuration file that can indicate to the IDE low level chip parameters such as memory space and allow it to display/read/write the registers of peripherals |
| 			  	        | T-8     	| maybe | maybe |maybe|HAL MAY be able to be extended to support the CORE-V X Coprocessor Interface (CV-X-IF) |
| 			  	        | T-9     	| maybe | maybe |maybe|HAL MAY be able to be extended to support the CV-VEC coprocessor | 
| *Industry Adoption*	| IA-1     	|  N    | maybe | Y   |HAL SHOULD be adopted/implemented for other RISC-V devices | 	
| *Specification Rqmtns*| S-1     	|  Y    | Y     | Y   |HAL Specification License for CORE-V MUST be open-source or freely licensed | 			  	| T-2     		| 
| 				        | S-2     	|  Y    | Y     | Y   |Proprietary extensions to the HAL Specification and Implementation, such as for custom ISA extensions or proprietary chip, MUST be supportable/allowable under open-source license|
| 				        | S-3     	|  Y    | Y     | Y   |HAL Specification, user documentation, and system implementation documentation for CORE-V HAL MUST be available in English |
| 				        | S-4     	|  N    | N     | N   |HAL Specification MUST be published and managed by an industry open source or standards body, such as OpenHW, RISC-V International, or FOSSi |
| *Implementation Rqmtns*| IM-1    	|  -    | -     | -   |A complete open source reference implementation of the HAL for CORE-V MUST be a project deliverable |
| 				        | IM-2     	|  -    | -     | -   |FreeRTOS SHOULD be supported in the open source reference implementation of HAL for CORE-V |
| 				        | IM-3     	|  -    | -     | -   |Newlib SHOULD be supported in the open source reference implementation  of HAL for CORE-V |
| 				        | IM-3     	|  -    | -     | -   |The HAL reference implementation for CORE-V SHOULD be published by the body publishing the Specification |

## OpenHW Members/Participants committed to participate
| **Company** | **Participants or Contributor** |
| --- | --- |
| Alibaba | Vincent Cui, Yunhai Shang, Linfei Chen, Zhixing Chen, Wenmeng Zhang, Devid Chen |
| CMC | Olive |

## Project Leader(s)
### Technical Project Leader(s)

- Vincent Cui
- Olive Zhao
### Project Manager, if a PM is designated

- Yunhai Shang
## Next steps/Investigation towards Project Launch

- Investigation of Solution Alternatives
- Comparison against requirements
- Selection of approach
- Feature specification (for S/W projects, we create Feature Specification at Project Launch)
- High level schedule/component map, assessing if initial 3 month estimate can be met
- repository needs
- Discussion of initial contribution
- Selection of industry group to publish the specification and open source reference codes
- Selection of Open Source license for both specifation and open source reference codes
- Discussion of project methodology for specification
- HAL Implementation considerations/timelinefor CORE-V MCU project SDK
- Clarification of how HAL forms a component of SDK
- By Project Launch stage, we shall have decided which peripherals and core features will be developed in the first phase of the project
