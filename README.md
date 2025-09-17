# EXPERIMENT 3: Simulation of All Flip-Flops using Blocking Statement

## AIM
To design and simulate basic flip-flops (SR, D, JK, and T) using **blocking statements** in Verilog HDL, and verify their functionality through simulation in Vivado 2023.1.

## APPARATUS REQUIRED
- Vivado 2023.1
- Computer with HDL Simulator

## DESCRIPTION
Flip-flops are the basic memory elements in sequential circuits.  
In this experiment, different types of flip-flops (SR, D, JK, T) are modeled using **behavioral modeling** with **blocking assignment (`=`)** inside the `always` block.  
Blocking assignments execute sequentially in the given order, which makes it easier to describe simple synchronous circuits.

## PROCEDURE
1. Open **Vivado 2023.1**.  
2. Create a **New RTL Project** (e.g., `FlipFlop_Simulation`).  
3. Add Verilog source files for each flip-flop (SR, D, JK, T).  
4. Add a testbench file to verify all flip-flops.  
5. Run **Behavioral Simulation**.  
6. Observe waveforms of inputs and outputs for each flip-flop.  
7. Verify that outputs match the truth table.  
8. Save results and capture simulation screenshots.

---

## VERILOG CODE

### SR Flip-Flop (Blocking)
```verilog
module ff(s,r,clk,rst,q);
input s,r,clk,rst;
output reg q;
always @(posedge clk)
begin
    if(rst==1)
        q=0;
    else if(rst==1)
        q=q;
    else if(s==0 && r==0)
        q=1'b0;
    else if(s==0 && r==1)
        q=1'b1;
    else 
        q=1'bx; 
        
end       
endmodule
```
### SR Flip-Flop Test bench 
```verilog
`timescale 1ns/1ps
module tb_ff;
reg s,r,clk,rst;
wire q;
ff uut(s,r,clk,rst,q);
always #5 clk=~clk;
initial begin
clk=0;s=0;r=0;rst=1;
#10 rst=0;
#10 s=0;r=0;
#10 s=0;r=1;
#10 s=1;r=0;
#10 s=1;r=1;
#10 s=0;r=0;
#20 $finish;
end 
endmodule
```
#### SIMULATION OUTPUT

<img width="1920" height="1080" alt="Screenshot 2025-09-17 092800" src="https://github.com/user-attachments/assets/ebf06813-f691-41f5-b3c6-c76f6d35bd22" />

---

### JK Flip-Flop (Blocking)
```verilog
module ff(j,k,clk,rst,q);
input j,k,clk,rst;
output reg q;
always @ (posedge clk)
begin
   if(rst==1)
      q=1'b0;
   else if(j==0&&k==0)
      q=q;
   else if(j==0&&k==1)
      q=1'b0;
   else if(j==1&&k==1)
      q=1'b1;
   else
      q=~q;
end
endmodule
```
### JK Flip-Flop Test bench 
```verilog
`timescale 1ns/1ps
module tb_ff;
reg j,k,clk,rst;
wire q;
ff uut(j,k,clk,rst,q);
always #5 clk=~clk;
initial
begin
  clk=0;j=0;k=0;rst=1;
  #10 rst=0;
  #10 j=0;k=0;
  #10 j=0;k=1;
  #10 j=1;k=0;
  #10 j=1;k=1;
  #10 j=0;k=0;
  #20 $finish;
end 
endmodule
```
#### SIMULATION OUTPUT

<img width="1920" height="1080" alt="Screenshot 2025-09-17 091529" src="https://github.com/user-attachments/assets/754fb032-d7bb-4f1e-919e-824f0e52dac1" />

---
### D Flip-Flop (Blocking)
```verilog
module ff(clk,rst,D,Q);
input clk,rst,D;
output reg Q;
always @ (posedge clk)
begin
  if (rst==1)
     Q=0;
  else
     Q=D;
end
endmodule
```
### D Flip-Flop Test bench 
```verilog
`timescale 1ns / 1ps
module tb_ff;
  reg clk,rst,D;
  wire Q;
  ff uut(clk,rst,D,Q);
  always #5 clk=~clk;
  initial
  begin
    clk=0;
    D=0;
    rst=1;#10;
    rst=0;
    D=0; #10;
    D=1;
  end
endmodule
```

#### SIMULATION OUTPUT

<img width="1920" height="1080" alt="Screenshot 2025-09-17 095512" src="https://github.com/user-attachments/assets/9adb6af0-b1cf-45e8-934a-f0fab3b7bf89" />

---
### T Flip-Flop (Blocking)
```verilog
module ff(clk,rst,T,Q);
input clk,rst,T;
output reg Q;
always @ (posedge clk)
begin
  if (rst==1)
     Q=0;
  else if (T==0)
     Q=Q;
  else
     Q=~Q;
end
endmodule
```
### T Flip-Flop Test bench 
```verilog
`timescale 1ns / 1ps
module tb_ff;
  reg clk,rst,T;
  wire Q;
  ff uut(clk,rst,T,Q);
  always #5 clk=~clk;
  initial
  begin
    clk=0;
    T=0;
    rst=1;#10;
    rst=0;
    T=0; #10;
    T=1;
  end
endmodule
```

#### SIMULATION OUTPUT

<img width="1920" height="1080" alt="Screenshot 2025-09-17 093605" src="https://github.com/user-attachments/assets/7427fd2d-b79d-400c-b20e-50d09e04ccca" />

---

### RESULT

All flip-flops (SR, D, JK, T) were successfully simulated using blocking statements in Verilog HDL.
The outputs matched the expected truth table values, demonstrating correct sequential behavior.
