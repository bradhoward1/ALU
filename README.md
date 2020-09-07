# ALU

### Overview
An ALU, or arithmetic logic unit, is a circuit within your computer that performs all of the math and bitwise functions necessary on integer values. The ALU reads in two inputs and an opcode to determine what functions are performed on the two inputs and what is outputted by the unit. To understand how the ALU works in a more in-depth way, the following guide is provided.


### Inputs/Outputs
First, it is important to understand the inputs and outputs of the ALU. The ALU module is defined by the following input and output pins:
- data_operandA: 32-bit input, first data input to perform ALU functions on
- data_operandB: 32-bit input, second data input to perform ALU functions on
- ctrl_ALUopcode: 5-bit input, determines which data result the ALU outputs
- ctrl_shiftamt: 5-bit input, determines the shift amount when performing the functions logical left shift or arithmetic right shift
- data_result: 32-bit output, data result from the ALU determined by the ALU opcode
- isNotEqual: 1-bit output, determines if A and B are not equal to each other
- isLessThan: 1-bit output, determines if A is stricly less than B
- overflow: 1-bit output, determines if the ADD or SUBTRACT functions produce an overflow bit


### Components/ Functionality
The ALU is composed of all of the necessary components, including an adder, a subtractor, a bit-wise AND operator, a bit-wise OR operator, a logical left shifter, and an arithmetic right shifter. Along with these, the ALU also implements an `overflow` output pin that will be true only if overflow occurs after the ADD or SUBTRACT functions, as well as an `isLessThan` information output signal that asserts true only if the first input A is stricly less than the second input B, and an `isNotEqual` information output signal that asserts true only if the first input A and the second input B are not the same number. It is important to note that the `isLessThan` and `isNotEqual` information output signals only need to be correct after the SUBTRACT function. 


### Implementation
To implement all of the components of the ALU, the following thought process was utilized:
1. Design all of the intricacies of each separate function: for example, the logical left shifter requires the development of a component that shifts a number 16 bits, then a component that shifts a number 8 bits, and so on to 1 bit.
2. Once all of the microcomponents are all developed, then begin construction on the main components/ functions. I started by desigining the adder, then elaborated upon it to create the subtractor, then designed the AND operator, then designed the OR operator, then designed the logical left shifter, then finished by designing the arithmetic right shifter.
3. Following the construction of all of the main components of the ALU, I integrated them into the main circuit by calling upon each submodule within the main ALU module. 
4. With all of the main components present, it was necessary to decide which output was desired. This is where the ALU opcode comes in: considering we know which output routes to which opcode, it was necessary to utilize a 5-bit, 32-to-1 multiplexer to decide which function would actually be outputted by the ALU. The following outputs route to the following opcodes:
    1. ADD = 00000
    2. SUBTRACT = 00001
    3. AND = 00010
    4. OR = 00011
    5. SLL = 00100
    6. SRA = 00101
5. Once the outputs were correct, I needed to work on the `overflow`,  `isLessThan`, and `isNotEqual` outputs. The overflow was implemented within the adder, so it was only necessary to create a 2-to-1 multiplexer that chose between the overflow output from the adder or the overflow output from the subtractor. For the `isLessThan` and `isNotEqual` output pins, implementation was necessary within the main ALU module. I utilized a series of AND and OR gates to compare bits/signs, ultimately allowing me to properly check these functions.
6. With all of these components in place, the ALU was completed.


### Bugs
To my knowledge, no bugs were present. I performed roughly 35 tests for each functionality, and all of them passed. 
