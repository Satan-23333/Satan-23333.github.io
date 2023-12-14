---
title: Example
date: 2023-12-12 15:14:10
tags:
---
---
## 1 **Spec**
---
| 左对齐 | 右对齐 | 居中对齐 |
| :-----| ----: | :----: |
| 单元格 | 单元格 | 单元格 |
| 单元格 | 单元格 | 单元格 |
---
## 2 **Design**
---
### 2.1 *multiply.v*
``` Verilog
`timescale 1ns / 1ps

module multiply(             
	input         clk,        // 时钟
	input         mult_begin, // 乘法开始信号
	input  [31:0] mult_op1,   // 乘法源操作数1
	input  [31:0] mult_op2,   // 乘法源操作数2
	output [63:0] product,    // 乘积
	output        mult_end   // 乘法结束信号
);
	//乘法正在运算信号和结束信号
	reg mult_valid;
	reg  [31:0] multiplier;

	assign mult_end = mult_valid & ~(|multiplier); //乘法结束信号：乘数全0
endmodule
```

### 2.2 *testbench.v*
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
	always #5 clk = ~clk;

endmodule
```
---
## 3 **Log**
---
### 3.1 *Compile Log*<p align="right">**Errors: 0, Warnings: 0**</p>
```
Model Technology ModelSim SE-64 vlog 10.7 Compiler 2017.12 Dec  7 2017
Start time: 20:07:49 on Dec 01,2023
vlog -work work ./design/multiply.v ./design/testbench.v -l vcompile.txt 
-- Compiling module multiply
-- Compiling module tb

Top level modules:
	tb
End time: 20:07:49 on Dec 01,2023, Elapsed time: 0:00:00
Errors: 0, Warnings: 10
```

### 3.2 *Simulation Log*<p align="right">**Errors: 0, Warnings: 0**</p>
```
# vsim -voptargs="+acc" work.tb -l ./vsim.txt -wlf ./vsim.wlf 
# Start time: 20:07:49 on Dec 01,2023
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
#  ------ERROR. A mismatch has occurred-----,ERROR in          40
# 1 ERROR! See log above for details.
# quit
# End time: 20:07:50 on Dec 01,2023, Elapsed time: 0:00:01
# Errors: 0, Warnings: 0
```

### 3.3 *TestBench Output*
``` 
------ERROR. A mismatch has occurred-----,ERROR in          40
1 ERROR! See log above for details.
```
