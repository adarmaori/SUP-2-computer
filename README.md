#Description File: SUP-2 computer
This file is meant to summerize the important things about SUP-2 - the specs, the features, implementation notes etc.

## Introduction
The SUP series is a set of currently in progress projects, for me to learn about Verilog, and also processor and computer architectures. The final goal is to design a usable microcontroller, which I will then synthesize using an FPGA and hopefully use in a real-life project.
This specific processor is an important one, because for the first time I will have a large degree of creative room to design the thing myself. The first processor, SUP-1, was a 1-1 copy of an existing architercture, which can be found in the book "Digital Computational Electronics" by Albert Malvino. 
I don't expect this specific processor to be uploaded to an FPGA, but I'd like to learn about synthesizable Verilog, so I'll try to make this project synthesizable
## broad definitions and features
I expect SUP-2 to have:
* a 16-bit architecture.
* I think I'll go with a RISC approach to make my life easier.
* This also means I can have 64Kb of RAM.
* I have enough room in the instruction set to make a cool, capable ALU, so I'll probably do that.
* might add storage on this one. Might have some interesting things to do there.
* I had wanted to learn about memory management for a while now, I'm gonna check if it can be implemented on such a small architecture and give it a go.

## Instruction Set
I have 24-bits for every instruction. 16-bits for the instruction, and 16-bits for the parameter (usually a memory address, bus also could be a pair of registers or an immediate value). You wil notice a hage amount of unused opCodes, and that is for two reasons: Firstly, I'm lazy, and a 24-bit instruction width is convenient for a 16-bit system but is a huge overkill. Secondly, this free space is an excellent place to put upgrades and future ideas without fearing for the instruction set maximum size, which is around 256 (I'm saying "around" because some opCodes will be deliberately empty).

The instructions I need:

### MOV:
there are 6 diiferent kinds of MOV we'll need to implement:
1. MOV immediate value to register: opCode 0x00
2. MOV memory address to register: opCode 0x01
3. MOV register to register: opCode 0x02
4. MOV immediate value to memory: opCode 0x03
5. MOV memory address to memory: opCode 0x04
6. MOV register to memory: opCode 0x05

### ALU:
I don't know yet how many operations the ALU will need, so I'll just give it 16 of them to be safe. As I said, this instruction set is built for rapid, guilt free upgrades and additions. However there is already a list of commands I'd like to implement:

1.   ADD: opCode 0x10
2.   SUB: opCode 0x11
3.   MUL: opCode 0x12
4.   DIV: opCode 0x13
5.   CMP: opCode 0x14
6.   AND: opCode 0x15
7.   OR:  opCode 0x16
8.   NOT: opCode 0x17
9.   XOR: opCode 0x18
10. NAND: opCode 0x19

### Conditionals:
Once again I'm not yet sure about the flags list or what exactly I'm gonna do with it. I have a fairly short list of ALU flags such as Carry, Zero and Negative, to which I'm gonna add the CMP flags like Greater, Smaller etc. I'm also not sure wether or not to add conditional commands other than conditional jumps. 
In any case, I think 32 commands will be more than enough, so opCodes 0x2x and 0x3x are available for those.
