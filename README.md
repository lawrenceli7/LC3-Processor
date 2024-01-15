# LC3-Processor using Logisim

The circuit I made is split into 4 main components:
1. The Main
2. The Control Unit
3. The ALU
4. Register File

Circuit's Purpose:
The processor is run by a clock that causes every state to change in the whole processor. The control unit 
increments the instruction register counts through the processes and counts the number of steps. The ALU is a
combinational circuit that primarily has 3 LC-3 operations: ADD, AND, and NOT. It calculates all three
of these operations given a certain input. It uses a multiplexer to pick the correct output based on the 
instruction specified. The Register File section of the circuit stores the value output of the main given the 
instruction specified. I also implemented more LC-3 instructions such as JMP, LD/LDR, and ST/STR, but ran into a 
problem with JMP instruction not properly working which I explained later on.

The test code in Assembly is:
ADD R2, R2 #6
ADD R1, R1, #6
AND R3, R2, R1
AND R1, R1, #0
ADD R4, R3, R2
NOT R1, R1
JMP R4

.FILL x0000
.FILL x0000
.FILL x0000
.FILL x0000
.FILL x0000

ST R4, x0015
STR R2, R2, #15
LD R5, x0015
LDR R6, R3, #15

The code in hex tested for inputs to the RAM is:
14a6 1266 5681 
5260 18c2 927f 
c100 0000 0000 
0000 0000 0000 
3808 748f 2a06 
6ccf

Unusual Behavior:
Code is good for most instructions such as ADD, AND, NOT, ST/STR, and LD/LDR because they result in the correct
output of the instruction when you input the code in hex into the ram; however, for JMP instructions, the code 
does not work for some reason as it just keeps looping. It should jump to the next specific address instead 
of looping. The JMP instructions could be fixed by changing some stuff in the Main circuit and some 
changes in the Control Unit giving more time to find out the exact reason why it is causing this weird looping
to happen.
