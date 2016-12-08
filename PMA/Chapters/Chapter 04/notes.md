#Chapter 4: Notes

## A Crash Course in x86 Disassembly

- **Three Coding Levels in Malware Analysis**
  - Malware authors create programs at the high-level language level.
  - Malware authors use a compiler to generate machine code to be run by the CPU.
  - Reverse Engineers use a disassembler to generate assembly code.



## Six Different Levels of Abstraction

- **Level 01: Hardware**
  - The only physical level
  - Consists of electrical circuits that implement combinations of logical operators.
  - Cannot be easily manipulated by software


- **Level 02: Microcode**
  - Also known as firmware.
  - Operates only on the exact circuitry for which it was designed.
  - We usually don’t worry about the microcode when it comes to malware.


- **Level 03: Machine code**
  - Uses opcodes, hexadecimal digits that tell the processor what you want it to do.
  - Created when compiling a computer program written in a high-level language.


- **Level 04: Low-level languages**
  - Human-readable version of a computer architecture’s instruction set.
  - The most common low-level language is assembly language.
  - A disassembler generates low-level language text from machine code.
  - Many different dialects of assembly language exist.


- **Level 05: High-level languages**
  - Most computer programmers operate at or above this level.
  - Provides strong abstraction from the machine level.
  - Includes C, C++, and others.
  - Typically turned into machine code by a compiler.


- **Level 06: Interpreted languages**
  - Highest level of abstraction.
  - Includes C#, Perl, .NET, and Java.
  - Code at this level is not compiled into machine code; instead, it is translated into bytecode.
  - Bytecode is an intermediate representation that is specific to the programming language.
  - Bytecode runs in an interpreter, a program that translates bytecode into machine code on the fly.
  - It can handle errors and memory management on its own, independent of the OS.



## Reverse-Engineering

- **Binary reversing**
  - Malware is typically stored in binary form at the machine code level.
  - We use a disassemble to convert the machine code to assembly language.


- **Assembly language**
  - Each assembly dialect is typically used to program a single family of microprocessors
  - Common architecture dialects: x86, x64, SPARC, PowerPC, MIPS, and ARM
  - x86, also known as Intel IA-32, is the most common architecture for PC's



## x86 Architecture

- **Components**
  - The internals of the x86 architecture follows the Von Neumann architecture.
  - It contains three essential hardware components.
  - The central processing unit (CPU) executes code.
  - The main memory of the system (RAM) stores all data and code.
  - The I/O system interfaces with devices such as hard drives, keyboards, and monitors.


- **The CPU**
  - The CPU contains several components.
  - The control unit gets instructions to execute from RAM using a register (EIP)
  - Registers are the CPU’s basic data storage units.
  - The ALU executes an instruction and places the results in registers or memory.
  - The process of fetching and executing instructions is repeated as a program runs.


- **Main Memory**
  - Can be divided into four major sections.
  - Data contains values that are put in place when a program is initially loaded.
  - Code includes the instructions fetched by the CPU to execute.
  - Heap is used for dynamic memory during program execution.
  - Stack is used for local variables and function parameters, and to help control program flow.



## x86 Instructions

- **Instructions**
  - The building blocks of assembly programs.
  - Made of a mnemonic and zero or more operands.
  - the mnemonic is a word that identifies the instruction to execute, such as ```mov```
  - Operands are typically used to identify information used by the instruction.


- **Instruction Format**

  - ```mov ecx, 0x42```
  - Move the ASCII character 'A' into the ecx register.

| Mnemonic | Dest Operand | Src Operand |
|----------|--------------|-------------|
| mov      | ecx          | 0x42        |



## Opcodes and Endianness

- **Opcodes**
  - Instructions correspond to opcodes that tell the CPU which operation to perform.
  - This book and other sources use the term opcode for the entire machine instruction.
  - Intel technically defines the term opcode much more narrowly.

- **Endianness
  - The endianness of data describes how it is stored in memory.
  - "little-endian" - least significant byte is ordered first (at the smallest address).
  - "big-endian" - most significant byte is ordered first (at the smallest address).
  - network data uses big-endian
  - x86 program uses little-endian
  - Changing between endianness is something malware must do during network communication.

- **Operands**
  - "Immediate operands" are fixed values, such as ```0x42```
  - "Register operands" refer to registers, such as ecx
  - "Memory address operands" refer to a memory address that contains the value such as [eax]

- **Registers**
  - "General registers" are used by the CPU during execution.
  - "Segment registers" are used to track sections of memory.
  - "Status flags" are used to make decisions.
  - "Instruction pointers" are used to keep track of the next instruction to execute.


```
 Common x86 Registers

| General registers | Segment registers | Status register | Instruction pointer |
|-------------------|-------------------|-----------------|---------------------|
| EAX (AX, AH, AL)  | CS                | EFLAGS          | EIP                 |
| EBX (BX, BH, BL)  | SS                |                 |                     |
| ECX (CX, CH, CL)  | DS                |                 |                     |
| EDX (DX, DH, DL)  | ES                |                 |                     |
| EBP (BP)          | FS                |                 |                     |
| ESP (SP)          | GS                |                 |                     |
| ESI (SI)          |                   |                 |                     |
```

- **Flags**
  - ```ZF``` - Zero flag is set when the result of an operation is equal to zero
  - ```CF``` - Carry flag is set when the result of an operation is too large for the destination operand
  - ```SF``` - Sign flag is set when the result of an operation is negative
  - ```TF``` - Trap flag is for debugging. Execute one instruction at a time if this is set.


## Simple Instructions

- **The ```mov``` Instruction**
  - Used to move data from one location to another.
  - Can move data into registers or RAM.
  - The format is ```mov destination, source```

- **The ```lea``` Instruction**
  - “load effective address” is similar to mov
  - The format of the instruction is ```lea destination, source```
  - Used to put a memory address into the destination.

- **Addition/Subtraction**
  - Addition or subtraction adds or subtracts a value from a destination operand.
  - The format of the addition instruction is ```add destination, value```
  - The format of the subtraction instruction is ```sub destination, value```
  - The sub instruction modifies two important flags: ZF and CF
  - ZF is set if the result is zero.
  - CF is set if the destination is less than the value subtracted.
  - The ```inc``` and ```dec``` instructions increment or decrement a register by one.

- **Multiplication/Division**
  - Multiplication and division both act on a predefined register.
  - The command is the instruction, plus the value that the register will be multiplied or divided by.
  - The format of the mul instruction is ```mul value```
  - The ```mul value``` instruction always multiplies eax by value.
  - The result is stored as a 64-bit value across two registers: EDX and EAX.
  - EDX stores the most significant 32 bits of the operations
  - EAX stores the least significant 32 bits of the operations
  - The format of div instruction is ```div value```
  - The ```div value``` instruction divides the 64 bits across EDX and EAX by value.
  - The EDX and EAX registers must be set up appropriately before the division occurs.
  - The result of the division operation is stored in EAX, and the remainder is stored in EDX.

- **Conditionals**
  - Conditionals are instructions that perform comparisons.
  - The two most popular conditional instructions are ```test``` and ```cmp```
  - The ```test``` instruction is identical to the ```and``` instruction.
  - However, the operands involved in ```test``` are not modified by the instruction.
  - The ZF is typically the flag of interest after the ```test``` instruction
  - A test of something against itself is often used to check for NULL values
  - The ```cmp``` instruction is identical to the ```sub``` instruction
  - However, the operands involved in ```cmp``` are not affected.
  - The ```cmp``` instruction is used only to set the flags..
  - The ZF and CF may be changed as a result of the ```cmp``` instruction.

- **Branching**
  - A branch is a sequence of code that is conditionally executed.
  - branching is used to describe the control flow through the branches of a program.
  - The most popular way branching occurs is with jump instructions
  - The format ```jmp location``` causes the next instruction to be the one at ```location```
  - ```jmp``` is an unconditional jump, because execution will always jump
  - Conditional jumps use the flags to determine whether to jump or not
  - More than 30 different types of conditional jumps can be used

- **Rep Instructions**
  - Rep instructions are a set of instructions for manipulating data buffers.
  - Usually in the form of an array of bytes, but they can also be single or double words
  - Most common data buffer manipulation instructions are ```movsx```, ```cmpsx```, ```stosx```, and ```scasx```
  - In these, x = b, w, or d for byte, word, or double word, respectively
  - The ESI and EDI registers are used in these operations.
  - ESI is the source index register.
  - EDI is the destination index register.
  - ECX is used as the counting variable.
  - The ```rep``` instruction increments the ESI and EDI offsets, and decrements the ECX register.
  - The ```movsb``` instruction is used to move a sequence of bytes from one location to another
  - The ```cmpsb``` instruction is used to compare two sequences of bytes to determine whether they contain the same data.
  - The ```scasb``` instruction is used to search for a single value in a sequence of bytes.
  - The ```stosb``` instruction is used to store values in a location specified by EDI.


```
 Sample instructions

| Instruction          | Description                                                                                                                                                                                                                                                    |
|----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| mov eax, ebx         | Copies the contents of EBX into the EAX register                                                                                                                                                                                                               |
| mov eax, 0x42        | Copies the value 0x42 into the EAX register                                                                                                                                                                                                                    |
| mov eax, [0x4037C4]  | Copies the 4 bytes at the memory location 0x4037C4 into the EAX register                                                                                                                                                                                       |
| mov eax, [ebx]       | Copies the 4 bytes at the memory location specified by the EBX register into the EAX register                                                                                                                                                                  |
| mov eax, [ebx+esi*4] | Copies the 4 bytes at the memory location specified by the result of the equation ebx+esi*4 into the EAX register                                                                                                                                              |
| lea eax, [ebx+8]     | Put EBX+8 into EAX                                                                                                                                                                                                                                             |
| mov eax, [ebx+8]     | Loads the data at the memory address specified by EBX+8.                                                                                                                                                                                                       |
| sub eax, 0x10        | Subtracts 0x10 from EAX                                                                                                                                                                                                                                        |
| add eax, ebx         | Adds EBX to EAX and stores the result in EAX                                                                                                                                                                                                                   |
| inc edx              | Increments EDX by 1                                                                                                                                                                                                                                            |
| dec ecx              | Decrements ECX by 1                                                                                                                                                                                                                                            |
| mul 0x50             | Multiplies EAX by 0x50 and stores the result in EDX:EAX                                                                                                                                                                                                        |
| div 0x75             | Divides EDX:EAX by 0x75 and stores the result in EAX and the remainder in EDX                                                                                                                                                                                  |
| xor eax, eax         | Clears the EAX register                                                                                                                                                                                                                                        |
| or eax, 0x7575       | Performs the logical or operation on EAX with 0x7575                                                                                                                                                                                                           |
| shl eax, 2           | Shifts the EAX register to the left 2 bits                                                                                                                                                                                                                     |
| ror bl, 2            | Rotates the BL register to the right 2 bits                                                                                                                                                                                                                    |
| nop                  | Do nothing....                                                                                                                                                                                                                                                 |
| test eax, eax        | Sets the Zero Flag if the the result of the AND operation is zero.                                                                                                                                                                                             |
| jz loc               | Jump to specified location if ZF = 1.                                                                                                                                                                                                                          |
| jnz loc              | Jump to specified location if ZF = 0.                                                                                                                                                                                                                          |
| je loc               | Same as jz, but commonly used after a cmp instruction. Jump will occur if the destination operand equals the source operand.                                                                                                                                   |
| jne loc              | Same as jnz, but commonly used after a cmp. Jump will occur if the destination operand is not equal to the source operand.                                                                                                                                     |
| jg loc               | Performs signed comparison jump after a cmp if the destination operand is greater than the source operand.                                                                                                                                                     |
| jge loc              | Performs signed comparison jump after a cmp if the destination operand is greater than or equal to the source operand.                                                                                                                                         |
| ja loc               | Same as jg, but an unsigned comparison is performed.                                                                                                                                                                                                           |
| jae loc              | Same as jge, but an unsigned comparison is performed.                                                                                                                                                                                                          |
| jl loc               | Performs signed comparison jump after a cmp if the destination operand is less than the source operand.                                                                                                                                                        |
| jle loc              | Performs signed comparison jump after a cmp if the destination operand is less than or equal to the source operand                                                                                                                                             |
| jb loc               | Same as jl, but an unsigned comparison is performed.                                                                                                                                                                                                           |
| jbe loc              | Same as jle, but an unsigned comparison is performed.                                                                                                                                                                                                          |
| jo loc               | Jump if the previous instruction set the overflow flag (OF = 1).                                                                                                                                                                                               |
| js loc               | Jump if the sign flag is set (SF = 1).                                                                                                                                                                                                                         |
| jecxz loc            | Jump to location if ECX = 0.                                                                                                                                                                                                                                   |
| repe cmpsb           | Used to compare two data buffers. EDI and ESI must be set to the two buffer locations, and ECX must be set to the buffer length. The comparison will continue until ECX = 0 or the buffers are not equal.                                                      |
| rep stosb            | Used to initialize all bytes of a buffer to a certain value. EDI will contain the buffer location, and AL must contain the initialization value. This instruction is often seen used with xor eax, eax.                                                        |
| rep movsb            | Typically used to copy a buffer of bytes. ESI must be set to the source buffer address, EDI must be set to the destination buffer address, and ECX must contain the length to copy. Byte-by-byte copy will continue until ECX = 0.                             |
| repne scasb          | Used for searching a data buffer for a single byte. EDI must contain the address of the buffer, AL must contain the byte you are looking for, and ECX must be set to the buffer length. The comparison will continue until ECX = 0 or until the byte is found. |
```


## The Stack

- **The Stack**
  - A data structure characterized by pushing and popping.
  - Memory for functions, local variables, and flow control is stored in a stack.
  - A stack is a last in, first out (LIFO) structure.
  - ESP is the stack pointer and contains a memory address that points to the top of the stack.
  - The value of ESP changes as values are pushed on and popped off the stack.
  - EBP is the base pointer that stays consistent within a given function.
  - The program uses it as a placeholder to track of the location of local variables and parameters.
  - The stack is used for short-term storage only.
  - It frequently stores local variables, parameters, and the return address.  
  - The most common convention is for local variables and parameters to be referenced relative to EBP.

- **Function Calls**
  - Functions are portions of code within a program that perform a specific task.
  - Code calls and transfers execution to functions before returning to the calling code.
  - How the stack is utilized by a program is consistent throughout a given binary.
  - For now, we will focus on the most common convention, known as ```cdecl```
  - Functions contain a prologue—a few lines of code at the start of the function.
  - The prologue before a function prepares the stack and registers for use within the function
  - The epilogue after a function restores the stack/registers to their state before the function was called.

- **Function Calls Flow**
1. Arguments are placed on the stack using push instructions.
2. A function is called using ```call memory_location```. This causes the current instruction address (that is, the contents of the EIP register) to be pushed onto the stack. This address will be used to return to the main code when the function is finished. When the function begins, EIP is set to ```memory_location``` (the start of the function).
3. Through the use of a function prologue, space is allocated on the stack for local variables and EBP (the base pointer) is pushed onto the stack. This is done to save EBP for the calling function.
4. The function performs its work.
5. Through the use of a function epilogue, the stack is restored. ESP is adjusted to free the local variables, and EBP is restored so that the calling function can address its variables properly. The ```leave``` instruction can be used as an epilogue because it sets ESP to equal EBP and pops EBP off the stack.
6. The function returns by calling the ```ret``` instruction. This pops the return address off the stack and into EIP, so that the program will continue executing from where the original call was made.
7. The stack is adjusted to remove the arguments that were sent, unless they’ll be used again later.


## Intel x86 Architecture References

- **The Manuals**
  - http://www.intel.com/products/processor/manuals/index.htm
  - Volume 1: Basic Architecture
  - Volume 2A: Instruction Set Reference, A–M
  - Volume 2B: Instruction Set Reference, N–Z
  - Volume 3A: System Programming Guide, Part 1
  - Volume 3B: System Programming Guide, Part 2
  - Optimization Reference Manual