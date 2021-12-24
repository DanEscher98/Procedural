# Protection Rings and Negative Rings

In order to isolate the sensitive parts of the memory, from 80386
onwards the execution rings were added. Rings 1 and 2 are not usually
used in Windows and Linux. Paging (major part of the modern protection
model) only has a concept of privileged (ring 0, 1, 2) and
unprivileged. The intent by Intel for rings 1 and 2 was for the OS to
put device drivers at that level. Those rings are in a way "mostly"
privileged. They can access supervisor pages, but if they attempt to
use a privileged instruction, they still GPF like ring 3 would. Some
of the use is for example, VirtualBox that puts the guest kernel code
in ring 1. From the perspective of OS design, having multiple
privileged rings is an oddity of x86, most other CPUs only have two
modes (supervisor and user).

Negative rings are *conceptual* levels of privilege, not actual
processor protection rings.

## The Rings

### **Ring 3:** Applications

### **Ring 2:** Device drivers

i/o privileged code

### **Ring 1:** Device drivers

drivers, guest operating systems

### **Ring 0:** Kernel

### **Ring -1:** Hypervisor

Actually, there are no negative rings. Ring -1 is a nickname given to
the virtualization function of the CPU that allows to run a hypervisor capable of running several operating systems at the same time.

### **Ring -2:** SMM (System Management Mode)

This is an operation mode that exists form 80386 onwards. It's
executed when a special type of interruption called SMI occurs and
breaks all related code running in the highest privilege mode of all.

### **Ring -3:** ME (Intel Management Engine)

Also PSP (Platform Secure Processor) in AMD. This was created as an
additional element of control. While the AMD PSP is a Cortex A5 CPU,
the ME is a classic Intel Pentium, that is, we are talking about an
x86 inside a x86. His functions are:

- Have full access to the system RAM independently of the main CPU.
- Have direct access to the TCP/IP stack and network interfaces.
- Can send/receive packets over the network, even with the OS having
    this banned.
- It's active when the computer is hibernating and when the rest of
    the system is off.
- Can take control of the computer remotely via internet.


### **Microcode:**



### **Silicon:**


## Glossary of Acronyms

- AMD: Advanced Micro Devices
- ARM: Applications, Real-Time, Microcontroller
- DPL: Descriptor Privilege Level
- GPF: General Protection Fault
- IA: Intel Architecture
- ME: Intel Management Engine
- PSP: Platform Secure Processor, the AMD equivalent of ME
- SMI: System Management Interrupt
- SMM: System Management Mode

## Concepts

- Segment Descriptor Table
    -