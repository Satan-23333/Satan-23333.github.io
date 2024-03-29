---
title: Multiply
date: 2024-01-26 17:33:10
tags:
---
---
## 1 **Spec** ————A 32-bits Multiplier
---
### Input
| Signal | Bits | Function |
| :----:| :----: | :----: |
| clk | 1 | Clock |
| mult_begin | 1 | begin multiply signal |
| mult_op1 | 32 | 32bits multiplier |
| mult_op2 | 32 | 32bits multiplier |

### Output
| Signal | Bits | Function |
| :----:| :----: | :----: |
| product | 64 | multiply product |
| mult_end | 1 | end multiply signal |
---
## 2 **Design**
---
### 2.1 *testbench.v*
``` Verilog
`timescale 1ns / 1ps
`define cycles  40
module tb;

	// Inputs
	reg clk;
	reg mult_begin;
	reg [31:0] mult_op1;
	reg [31:0] mult_op2;
	reg [63:0] Data_in_t;
	// Outputs
	wire [63:0] product;
	wire mult_end;

	// Instantiate the Unit Under Test (UUT)
	multiply uut (
		.clk(clk), 
		.mult_begin(mult_begin), 
		.mult_op1(mult_op1), 
		.mult_op2(mult_op2), 
		.product(product), 
		.mult_end(mult_end)
	);
	integer i,errors[0:39],cnt;
	
	integer fd = 0;
	initial begin
		// Initialize Inputs
		clk = 0;
		mult_begin = 0;
		mult_op1 = 0;
		mult_op2 = 0;
		for (i = 0; i < 40; i = i + 1)
			begin
			errors[i] = 0;
			end
		i=0;
		cnt=0;
		$dumpfile("mul.vcd");

		$dumpvars();
		fd = $fopen("./report.txt", "w");
		// if(!fd)
		// 	begin
		// 		$display("Could not open File \r");
		// 		$stop;
		// 	end

		#1000;
		//正数*正数
		mult_begin = 1;
		mult_op1 = 32'H6A98F28D;
		mult_op2 = 32'H7E184AD4;
		Data_in_t = 64'H348164E09FFD9EC4;
		#50;
		mult_begin = 0;
		#1000;
		mult_begin = 1;
		mult_op1 = 32'H2B661ACE;
		mult_op2 = 32'H6AE5B749;
		Data_in_t = 64'H121F3881A38CE6BE;
		#50;
		mult_begin = 0;
		#1000;
		mult_begin = 1;
		mult_op1 = 32'H25BD7BEE;
		mult_op2 = 32'H4ADDFFD9;
		Data_in_t = 64'H0B09801E84861EBE;
		#50;
		mult_begin = 0;
		#1000;
		mult_begin = 1;
		mult_op1 = 32'H0D3A404E;
		mult_op2 = 32'H64B23883;
		Data_in_t = 64'H0533F68AB11BF7EA;
		#50;
		mult_begin = 0;
		#1000;
		mult_begin = 1;
		mult_op1 = 32'H3F64172B;
		mult_op2 = 32'H60CE4AB1;
		Data_in_t = 64'H17F89DB9878072BB;
		#50;
		mult_begin = 0;
		#1000;
		mult_begin = 1;
		mult_op1 = 32'H16761A51;
		mult_op2 = 32'H13462A55;
		Data_in_t = 64'H01B0EBF60AAE06E5;
		#50;
		mult_begin = 0;
		#1000;
		mult_begin = 1;
		mult_op1 = 32'H2026D659;
		mult_op2 = 32'H6D726BE8;
		Data_in_t = 64'H0DBEE81CB76B73A8;
		#50;
		mult_begin = 0;
		#1000;
		mult_begin = 1;
		mult_op1 = 32'H02618586;
		mult_op2 = 32'H1E83A59C;
		Data_in_t = 64'H0048A717560EBBA8;
		#50;
		mult_begin = 0;
		#1000;
		mult_begin = 1;
		mult_op1 = 32'H1B77F796;
		mult_op2 = 32'H5B4B942D;
		Data_in_t = 64'H09CBC10E0A2B3D5E;
		#50;
		mult_begin = 0;
		#1000;
		mult_begin = 1;
		mult_op1 = 32'H5AC08456;
		mult_op2 = 32'H64ED2634;
		Data_in_t = 64'H23C745771E5DA578;
		#50;
		mult_begin = 0;
		#1000;
		//负数*负数
		mult_begin = 1;
		mult_op1 = 32'HDC7F53A9;
		mult_op2 = 32'H9F5CEA89;
		Data_in_t = 64'H0D66DE886A583F71;
		#50;
		mult_begin = 0;
		#1000;
		mult_begin = 1;
		mult_op1 = 32'HB7AC2234;
		mult_op2 = 32'HD3FCAAC7;
		Data_in_t = 64'H0C6F5B2E9CB51E6C;
		#50;
		mult_begin = 0;
		#1000;
		mult_begin = 1;
		mult_op1 = 32'HDAE39537;
		mult_op2 = 32'HD347F65B;
		Data_in_t = 64'H067B902D3789E48D;
		#50;
		mult_begin = 0;
		#1000;
		mult_begin = 1;
		mult_op1 = 32'H9F1D7AEA;
		mult_op2 = 32'HFA3E1FC8;
		Data_in_t = 64'H022DCC3B29965CD0;
		#50;
		mult_begin = 0;
		#1000;
		mult_begin = 1;
		mult_op1 = 32'H9F09D52B;
		mult_op2 = 32'H99A59337;
		Data_in_t = 64'H26C454CFE83B7D3D;
		#50;
		mult_begin = 0;
		#1000;
		mult_begin = 1;
		mult_op1 = 32'H90E87B84;
		mult_op2 = 32'HEAA39889;
		Data_in_t = 64'H09450737E2CC79A4;
		#50;
		mult_begin = 0;
		#1000;
		mult_begin = 1;
		mult_op1 = 32'HEA722216;
		mult_op2 = 32'HF7B63872;
		Data_in_t = 64'H00B2A530D3EBFDCC;
		#50;
		mult_begin = 0;
		#1000;
		mult_begin = 1;
		mult_op1 = 32'HB25BF9E7;
		mult_op2 = 32'H9EAEE22C;
		Data_in_t = 64'H1D83C041476EE1B4;
		#50;
		mult_begin = 0;
		#1000;
		mult_begin = 1;
		mult_op1 = 32'HE23F69BC;
		mult_op2 = 32'H804F5678;
		Data_in_t = 64'H0ED712A6FC42B820;
		#50;
		mult_begin = 0;
		#1000;
		mult_begin = 1;
		mult_op1 = 32'H81A763DE;
		mult_op2 = 32'HE857F5F4;
		Data_in_t = 64'H0BACE522E690A598;
		#50;
		mult_begin = 0;
		#1000;
		//正数*负数
		mult_begin = 1;
		mult_op1 = 32'H117B72B5;
		mult_op2 = 32'HFDE88F42;
		Data_in_t = 64'HFFDB6F504BEEADAA;
		#50;
		mult_begin = 0;
		#1000;
		mult_begin = 1;
		mult_op1 = 32'H2EF80EBF;
		mult_op2 = 32'HDE0A0A5F;
		Data_in_t = 64'HF9C4E5A25416EEE1;
		#50;
		mult_begin = 0;
		#1000;
		mult_begin = 1;
		mult_op1 = 32'H56FA268C;
		mult_op2 = 32'H86F6EBA9;
		Data_in_t = 64'HD6E0AE135F0DF66C;
		#50;
		mult_begin = 0;
		#1000;
		mult_begin = 1;
		mult_op1 = 32'H77A17497;
		mult_op2 = 32'HD367D395;
		Data_in_t = 64'HEB29235711D250E3;
		#50;
		mult_begin = 0;
		#1000;
		mult_begin = 1;
		mult_op1 = 32'H5DE04686;
		mult_op2 = 32'HD29727E2;
		Data_in_t = 64'HEF59213D8FC6AC4C;
		#50;
		mult_begin = 0;
		#1000;
		mult_begin = 1;
		mult_op1 = 32'H0F50B083;
		mult_op2 = 32'H844E2D5D;
		Data_in_t = 64'HF89997CD13412697;
		#50;
		mult_begin = 0;
		#1000;
		mult_begin = 1;
		mult_op1 = 32'H671294E9;
		mult_op2 = 32'HE6CCC285;
		Data_in_t = 64'HF5DA8E00A12BEF0D;
		#50;
		mult_begin = 0;
		#1000;
		mult_begin = 1;
		mult_op1 = 32'H23B50CC7;
		mult_op2 = 32'HCFD68C3B;
		Data_in_t = 64'HF9484575D510C5DD;
		#50;
		mult_begin = 0;
		#1000;
		mult_begin = 1;
		mult_op1 = 32'H60F5B7D8;
		mult_op2 = 32'HFA36D021;
		Data_in_t = 64'HFDCF0059DC9C32D8;
		#50;
		mult_begin = 0;
		#1000;
		mult_begin = 1;
		mult_op1 = 32'H4E520906;
		mult_op2 = 32'HC45F3B23;
		Data_in_t = 64'HEDC1E86B8E859DD2;
		#50;
		mult_begin = 0;
		#1000;
		//0*随机
		mult_begin = 1;
		mult_op1 = 32'H00000000;
		mult_op2 = 32'H51B64CC8;
		Data_in_t = 64'H0000000000000000;
		#50;
		mult_begin = 0;
		#1000;
		mult_begin = 1;
		mult_op1 = 32'H00000000;
		mult_op2 = 32'H7BA49B33;
		Data_in_t = 64'H0000000000000000;
		#50;
		mult_begin = 0;
		#1000;
		mult_begin = 1;
		mult_op1 = 32'H00000000;
		mult_op2 = 32'HF937655D;
		Data_in_t = 64'H0000000000000000;
		#50;
		mult_begin = 0;
		#1000;
		mult_begin = 1;
		mult_op1 = 32'H00000000;
		mult_op2 = 32'H72061A95;
		Data_in_t = 64'H0000000000000000;
		#50;
		mult_begin = 0;
		#1000;
		mult_begin = 1;
		mult_op1 = 32'H00000000;
		mult_op2 = 32'HA31321B7;
		Data_in_t = 64'H0000000000000000;
		#50;
		mult_begin = 0;
		#1000;
		mult_begin = 1;
		mult_op1 = 32'H00000000;
		mult_op2 = 32'H8532E4B1;
		Data_in_t = 64'H0000000000000000;
		#50;
		mult_begin = 0;
		#1000;
		mult_begin = 1;
		mult_op1 = 32'H00000000;
		mult_op2 = 32'HCC480B3E;
		Data_in_t = 64'H0000000000000000;
		#50;
		mult_begin = 0;
		#1000;
		mult_begin = 1;
		mult_op1 = 32'H00000000;
		mult_op2 = 32'HB712E17B;
		Data_in_t = 64'H0000000000000000;
		#50;
		mult_begin = 0;
		#1000;
		mult_begin = 1;
		mult_op1 = 32'H00000000;
		mult_op2 = 32'HFF3BAF67;
		Data_in_t = 64'H0000000000000000;
		#50;
		mult_begin = 0;
		#1000;
		mult_begin = 1;
		mult_op1 = 32'H00000000;
		mult_op2 = 32'H6D0E5A16;
		Data_in_t = 64'H0000000000000000;
		#50;
		mult_begin = 0;

		#500;
		if (cnt == 0)
		begin
			$display("Simulation finished Successfully.");
			$fdisplay(fd, "Simulation finished Successfully.");
		end
		else if (cnt >= 1)
		begin	
			$display("%0d ERROR! See log for details.",cnt);
			$fdisplay(fd, "%0d ERROR! See log above for details.",cnt) ;
		end
		$fclose(fd);

		// $finish;
	end
   always #5 clk = ~clk;

//比较
	always @ (negedge mult_end)
		begin
		if ( product !== Data_in_t || product == 64'Bz )
			begin
			// $display(" ------ERROR. A mismatch has occurred-----,ERROR in ", i);
			$fdisplay(fd," ------ERROR. A mismatch has occurred-----,ERROR in ", i);
			errors[i-1] =  1;
			cnt = cnt + 1;
			end
		i = i + 1; 
		
		end
endmodule

```
### 2.2 *updated_design_0.v*
``` Verilog

`timescale 1ns / 1ps   

module multiply(               
    input         clk,        // Clock
    input         mult_begin, // begin multiply signal
    input  [31:0] mult_op1,   // 32bits multiplier
    input  [31:0] mult_op2,   // 32bits multiplier
    output [63:0] product,    // multiply product
    output        mult_end   // end multiply signal
);  
    // Multiplication operation signals
    reg mult_valid;  
    reg  [31:0] multiplier;  

    assign mult_end = mult_valid & ~(|multiplier); // End signal: when multiplier is all zeros
    always @(posedge clk)     
    begin  
        if (multiplier == 32'd0)  
        begin  
            mult_valid <= 1'b0;     // No valid multiplication operation
        end  
        else  
        begin  
            mult_valid <= 1'b1;  
        end  
    end  

    // Absolute values of operands
    wire        op1_sign;      // Sign of operand 1
    wire        op2_sign;      // Sign of operand 2
    wire [31:0] op1_absolute;  // Absolute value of operand 1
    wire [31:0] op2_absolute;  // Absolute value of operand 2
    assign op1_sign = mult_op1[31];  
    assign op2_sign = mult_op2[31];  
    assign op1_absolute = op1_sign ? (~mult_op1+1) : mult_op1;  
    assign op2_absolute = op2_sign ? (~mult_op2+1) : mult_op2;  

    // Loading multiplicand and shifting
    reg  [63:0] multiplicand;  
    always @ (posedge clk)    
    begin  
        if (mult_valid)  
        begin    // Shift multiplicand left by one bit each clock cycle
            multiplicand <= {multiplicand[62:0],1'b0};  
        end  
        else if (mult_begin)   
        begin   // Load multiplicand with absolute value of operand 1
            multiplicand <= {32'd0,op1_absolute};  
        end  
    end  

    // Loading multiplier and shifting
    always @ (posedge clk)   
    begin  
        if(mult_valid)  
        begin       // Shift multiplier right by one bit each clock cycle
            multiplier <= {1'b0,multiplier[31:1]}; 
        end  
        else if(mult_begin)  
        begin   // Load multiplier with absolute value of operand 2
            multiplier <= op2_absolute;  
        end  
    end  

    // Partial product calculation
    wire [63:0] partial_product;  
    assign partial_product = multiplier[0] ? multiplicand : 64'd0;        

    // Accumulator for the product
    reg [63:0] product_temp;		
    always @ (posedge clk)  
    begin  
        if (mult_valid)  
        begin  
            product_temp <= product_temp + partial_product;  
        end        
        else if (mult_begin)  
        begin  
            product_temp <= 64'd0;  
        end  
     end  

    // Product sign and final result
    reg product_sign;	// Sign of the product
    always @ (posedge clk)    
    begin  
        if (mult_valid)  
        begin  
            product_sign <= op1_sign ^ op2_sign; // Calculating sign of the product
        end  
    end   
    assign product = product_sign ? (~product_temp+1) : product_temp; // Adjusting sign of the product
endmodule  
```
---
## 3 **Report**
---
### 3.1 *Compile Report*<p align="right">**Errors: 0, Warnings: 0**</p>
```
Model Technology ModelSim SE-64 vlog 10.7 Compiler 2017.12 Dec  7 2017
Start time: 17:33:09 on Jan 26,2024
vlog -work work ./design/testbench.v ./design/updated_design_0.v -l vcompile.txt 
-- Compiling module tb
-- Compiling module multiply

Top level modules:
	tb
End time: 17:33:09 on Jan 26,2024, Elapsed time: 0:00:00
Errors: 0, Warnings: 0
```
### 3.2 *Simulation Report*<p align="right">**Errors: 0, Warnings: 0**</p>
```
# vsim -voptargs="+acc" work.tb -l ./vsim.txt -wlf ./vsim.wlf 
# Start time: 17:33:09 on Jan 26,2024
# ** Note: (vsim-8009) Loading existing optimized design _opt2
# //  ModelSim SE-64 10.7 Dec  7 2017
# //
# //  Copyright 1991-2017 Mentor Graphics Corporation
# //  All Rights Reserved.
# //
# //  ModelSim SE-64 and its associated documentation contain trade
# //  secrets and commercial or financial information that are the property of
# //  Mentor Graphics Corporation and are privileged, confidential,
# //  and exempt from disclosure under the Freedom of Information Act,
# //  5 U.S.C. Section 552. Furthermore, this information
# //  is prohibited from disclosure under the Trade Secrets Act,
# //  18 U.S.C. Section 1905.
# //
# Loading work.tb(fast)
# Loading work.multiply(fast)
# Simulation finished Successfully.
# quit
# End time: 17:33:10 on Jan 26,2024, Elapsed time: 0:00:01
# Errors: 0, Warnings: 0
```
### 3.3 *TestBench Report*
```
Simulation finished Successfully.
```
