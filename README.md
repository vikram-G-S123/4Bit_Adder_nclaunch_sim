# EXP1: 4 Bit Adder functionality verification

## Aim:
To write a verilog code for 4bit adder and verify the functionality using Test bench.

 Write Verilog Code

 Verify the Functionality using Test-bench.

## Tool Required: 
Functional Simulation: nclaunch Simulator (nclaunch) 

## 4-bit Adder Design:
To construct a 4-bit adder, need to chain together four 1-bit full adders. Each full adder computes the sum and carry for one bit of the two numbers. The carry-out from one adder feeds into the carry-in of the next adder in the sequence. This process adds the two 4-bit numbers bit by bit, with the carry propagating through each stage, resulting in a final sum and carry-out at the end.

To design a 1-bit full adder, the first step is to create a truth table that represents all possible combinations of the inputs (A, B, and CIN) and the corresponding outputs (Sum(S) and COUT).

![image](https://github.com/user-attachments/assets/716a26b6-a449-42e0-9e2d-cdbaa4b291b9)

Here’s the truth table for a 1-bit full adder:

![tt](https://github.com/user-attachments/assets/0b3ab24f-1d7e-4a01-80ce-5e7406f4082b)

### Fig 1 : Diagram and truth table of full adder

### Logic Expressions:

1.	Sum (S):
   
S=A⊕B⊕CIN

Where ⊕ represents XOR.

3.	Carry out (COUT):
   
COUT=(A&B) | (CIN&(A^B))

![image](https://github.com/user-attachments/assets/7d6fa554-2614-4f19-aa68-65c9e6153caa)

### Fig 2:Diagram of 4 Bit Adder

## Creating Source Codes 

	In the Terminal, type gedit <filename>.v (ex: gedit 4bitadder.v). 

	A Blank Document opens up into which the following source code can be typed down. 

Note : File name should be with HDL Extension

### a) Verify the Functionality 



`timescale 1ns / 1ps

module four_bit_adder (
    input [3:0] A,    
    input [3:0] B,    
    input Cin,        
    output [3:0] Sum, 
    output Cout       
);

    assign {Cout, Sum} = A + B + Cin;  
endmodule

TESTBENCH:

`timescale 1ns / 1ps

module testbench;

    reg [3:0] A, B;
    reg Cin;
    wire [3:0] Sum;
    wire Cout;
    
    four_bit_adder uut (
        .A(A), .B(B), .Cin(Cin),
        .Sum(Sum), .Cout(Cout)
    );

    initial begin
        $monitor("A = %b, B = %b, Cin = %b | Sum = %b, Cout = %b", A, B, Cin, Sum, Cout);
        

        A = 4'b0001; B = 4'b0010; Cin = 1'b0; #10;
        A = 4'b0101; B = 4'b0110; Cin = 1'b1; #10;
        A = 4'b1111; B = 4'b0001; Cin = 1'b0; #10;
        A = 4'b1010; B = 4'b0101; Cin = 1'b1; #10;
        
        $finish;
    end
endmodule

## Functional Simulation: 


![Screenshot 2025-04-22 174706](https://github.com/user-attachments/assets/5dc02f15-8490-4cc9-aaa1-44265bb45a92)


### Fig 3:Invoke the Cadence Environment

![Screenshot 2025-04-22 174706](https://github.com/user-attachments/assets/e2c5d712-ac72-441a-bd8d-0933f5a05ba2)


### Fig 4:Setting Multi-step simulation

 ![Screenshot 2025-04-22 174941](https://github.com/user-attachments/assets/eaa44870-3de0-42b8-afd0-609e6276c172)


### Fig 5:cds.lib file Creation

![Screenshot 2025-04-22 174951](https://github.com/user-attachments/assets/d1fa439e-643b-4dfe-beab-9ae5ea82477e)


### Fig 6: Selection of Don’t include any libraries

	A ‘NCLaunch window’ appears as shown in figure below 

	Left side you can see the HDL files. Right side of the window has worklib and snapshots directories listed. 

	Worklib is the directory where all the compiled codes are stored while Snapshot will have output of elaboration which in turn goes for simulation .

	To perform the function simulation, the following three steps are involved Compilation, Elaboration and Simulation. 

### Fig 7: Nclaunch Window



## Step 1: Compilation:– Process to check the correct Verilog language syntax and usage 

	Inputs: Supplied are Verilog design and test bench codes 

	Outputs: Compiled database created in mapped library if successful, generates report else error reported in log file 

	Steps for compilation: 

1. Create work/library directory (most of the latest simulation tools creates automatically) 
2. Map the work to library created (most of the latest simulation tools creates automatically) 
3. Run the compile command with compile options 
i.e Cadence IES command for compile: ncverilog +access+rwc -compile fa.v

Left side select the file and in Tools : launch verilog compiler with current selection will get enable. Click it to compile the code 

Worklib is the directory where all the compiled codes are stored while Snapshot will have output of elaboration which in turn goes for simulation

### Fig 8: Compiled database in worklib

	After compilation it will come under worklib you can see in right side window

	Select the test bench and compile it. It will come under worklib. Under Worklib you can see the module and test-bench. 

	The cds.lib file is an ASCII text file. It defines which libraries are accessible and where they are located. It contains statements that map logical library names to their physical directory paths. For this Design, you will define a library called “worklib”

## Step 2: Elaboration:– To check the port connections in hierarchical design 
	Inputs: Top level design / test bench Verilog codes 

	Outputs: Elaborate database updated in mapped library if successful, generates report else error reported in log file 

	Steps for elaboration – Run the elaboration command with elaborate options 

1.	It builds the module hierarchy 
2.	Binds modules to module instances 
3.	Computes parameter values 
4.	Checks for hierarchical names conflicts 
5.	It also establishes net connectivity and prepares all of this for simulation
   
	After elaboration the file will come under snapshot. Select the test bench and elaborate it.


## Step 3: Simulation: – Simulate with the given test vectors over a period of time to observe the output behaviour. 

	Inputs: Compiled and Elaborated top level module name 

	Outputs: Simulation log file, waveforms for debugging 

	Simulation allow to dump design and test bench signals into a waveform 

	Steps for simulation – Run the simulation command with simulator options

![Screenshot 2025-04-22 173401](https://github.com/user-attachments/assets/a2db33a1-5bea-4add-b506-6b585b6e51fe)


### Result:

The functionality of a 4-bit adder was successfully verified using a test bench and simulated with the nclaunch tool.















