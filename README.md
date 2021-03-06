#Instruction Set Architecture

Addressing modes: 	immediate and displacement
Data types: 		32-bit words
Instruction formats:	I,R,J type instructions

## ARITHMETIC, LOGIC AND LOADS - CATEGORY 0

ADD  	R1, R2, R3		| R1 <- R2 + R3
ADDI	R1, R2, CONST16 | R1 <- R2 + CONST16
MOV	R1, R2				| R1 <- R2
NEG	R1, R2				| R1 <- -1*R2
SUB	R1, R2, R3			| R1 <- R2-R3
SUBI	R1, R2, CONST	| R1 <- R2-CONST

SL	R1, R2, SHIFT5		| R1 <- R2 << SHIFT5
SR	R1, R2, SHIFT5		| R1 <- R2 >> SHIFT5

MUL	R1, R2, R3			| R1 <- R2, R3

AND	R1, R2, R3			| R1 <- R2 & R3
OR	R1, R2, R3			| R1 <- R2 | R3
XOR	R1, R2, R3			| R1 <- R2 XOR R3
NOT	R1, R2				| R1 <- ~R2

NOP

LD 	R1, OFF16, R2 	| Load reg location with offset :: R1 <- MEM[R2+1000]
*LDI	R1, OFF16	| Load from immediate operand   :: R1 <- MEM[1000]

## STORES AND LOADS - CATEGORY 1

STR	R1, 60, R2	| Store with offset		:: MEM[R2+60] <- R1

// TODO: add support for floating point and more data types

## CONTROL FLOW - CATEGORY 2

B	name		| Branch
*JR	R3		| Jump to reg

BEQ	R3, R4, name	| Branch if r4==r3
*BNE	R3, R4, name	| Branch if r4!=r3
BLTH	R1, R2, name	| Branch if R1<R2 to name

## SPECIAL - CATEGORY 3


BREAK imm		| Cause a breakpoint exception
.word imm		| stores a 32-bit value directly into memory address

Note: all operands beginning with R refer to a concrete physical register
TYPE 0 - store into leftmost reg
TYPE 1 - store leftmost reg into memory location on rhs

# Compilation

    javac *.java

# Execution

    java Simulator <filename> <[1/0] dynamic branch prediction on/off>

Example:
    java Simulator finite_field_inversion.asm 1

Note:
Press enter to step through each clock cycle. 'f' and enter will finish the
current program

# Test Programs

branch_test.asm
features.asm
bubbleSort.asm
fibs.asm
instruction_test.asm
renaming_test.asm
vadd.asm
vector_xor.asm

# Benchmarks

benchmark 1: fibsSSOptimised.asm

benchmark 2a: inner_product.asm
benchmark 2b: inner_product unrolled.asm

benchmark 3: bubbleSort.asm vs. bubbleSortOptimised.asm

benchmark 4: hydro_fragment_forward_branch.asm

benchmark 5a: finite field inversion.asm
benchmark 5b: finite field redundancy.asm
