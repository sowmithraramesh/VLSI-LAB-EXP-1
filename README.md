
## AIM: 
     To simulate and synthesis Logic Gates,Adders and Subtractor using Xilinx ISE.

## APPARATUS REQUIRED: 
      Xilinx 14.7 Spartan6 FPGA

## PROCEDURE:
##### STEP:1 Start the Xilinx navigator, Select and Name the New project.
##### STEP:2 Select the device family, device, package and speed. 
##### STEP:3 Select new source in the New Project and select Verilog Module as the Source type.
##### STEP:4 Type the File Name and Click Next and then finish button. Type the code and save it.
##### STEP:5 Select the Behavioral Simulation in the Source Window and click the check syntax. 
##### STEP:6 Click the simulation to simulate the program and give the inputs and verify the outputs as per the truth table. 
##### STEP:7 Select the Implementation in the Sources Window and select the required file in the Processes Window. 
##### STEP:8 Select Check Syntax from the Synthesize XST Process. Double Click in the Floorplan Area/IO/Logic-Post Synthesis process in the User Constraints process group. UCF(User constraint File) is obtained. ##### STEP:9 In the Design Object List Window, enter the pin location for each pin in the Loc column Select save from the File menu. 
##### STEP:10 Double click on the Implement Design and double click on the Generate Programming File to create a bitstream of the design.(.v) file is converted into .bit file here.
##### STEP:11 Load the Bit file into the SPARTAN 6 FPGA
##### STEP:12 On the board, by giving required input, the LEDs starts to glow light, indicating the output.


## LOGIC GATES:

### LOGIC DIAGRAM:
![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/ee17970c-3ac9-4603-881b-88e2825f41a4)

### VERILOG CODE:
```
module LG (a, b, c0, c1, c2, c3, c4, c5, c6);
input a, b; output c0, c1, c2, c3, c4, c5, c6; 
and (c0, a, b); 
or (c1, a, b); 
xor (c2, a, b); 
nand (c3, a, b);
nor (c4, a, b); 
xnor (c5, a, b); 
not (c6, a); 
endmodule
```
### OUTPUT:
![image](https://github.com/sowmithraramesh/VLSI-LAB-EXP-1/assets/166893766/dea9cd7a-e6be-41e4-98d8-208b0c78526d)

## HALF ADDER:

### LOGIC DIAGRAM:
![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/0e1ecb96-0c25-4556-832b-aeeedfdfe7b9)
### VERILOG CODE:
```
module HA (a, b, sum, carry); 
input a, b;
output sum, carry; 
xor g1(sum, a, b); 
and g2 (carry, a, b);
endmodule
```
### OUTPUT:
![image](https://github.com/sowmithraramesh/VLSI-LAB-EXP-1/assets/166893766/3bdadd5b-0027-456e-af84-252f16d4637c)

## FULL ADDER:

### LOGIC DIAGRAM:
![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/9bb3964c-438f-469d-a3de-c1cca6f323fb)

### VERILOG CODE:
```
module FA(a, b, c, sum, carry);
input a, b, c; 
output sum, carry; 
wire w1, w2, w3; 
xor g1(w1, a, b); 
and g2(w2, a, b); 
xor g3(sum, w1 ,c); 
and g4(w3, w1, c);
or g5(carry, w3, w2); 
endmodule

```
### OUTPUT:
![image](https://github.com/sowmithraramesh/VLSI-LAB-EXP-1/assets/166893766/a74a92a0-2b99-4517-bffe-547b21f4c88e)

## HALF SUBRACTOR:

### LOGIC DIAGRAM:
![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/731470b7-eb4e-49f8-8bb7-2994052a7184)

### VERILOG CODE:
```
module HS (a, b, diff, borrow);
input a, b; 
output diff, borrow;
xor gl (diff, a, b); 
and g2 (borrow, ~a, b);
endmodule
```
### OUTPUT:
![image](https://github.com/sowmithraramesh/VLSI-LAB-EXP-1/assets/166893766/9402de46-0e98-48bb-b572-6f5acd7a7612)

## FULL SUBRACTOR:

### LOGIC DIAGRAM
![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/d66f874b-c1f2-44b3-a035-7149b56430c1)

### VERILOG CODE:
```
module FS(a, b, c, diff, borrow); 
input a, b, c;
output diff, borrow; 
wire x, y, z; 
xor g1(x, a, b);
and g2(y, ~a , b);
xor g3(diff, x, c);
and g4(z, c, ~x);
or g5(borrow, y, z);
endmodule
```
### OUTPUT:
![image](https://github.com/sowmithraramesh/VLSI-LAB-EXP-1/assets/166893766/a199494a-90f0-423d-9de8-472136ef9908)

## 8-BIT-RIPPLE-CARRY-ADDER 

### LOGIC DIAGRAM
![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/7385a408-40a5-4203-8050-b72818622d79)

### VERILOG CODE:
```
module FA(a, b, c, sum, carry); 
input a, b, c;
output sum, carry; 
assign sum=a ^ b ^ c;
assign carry=a & b|b & c|a & c;
endmodule 
module RCA(a, b, c, sum, carry);
input [7:0] a, b; 
input c; 
output [7:0] sum;
output carry;
wire [6:0] w;
FA f1(a[0], b[0], c, sum[0], w[0]); 
FA f2(a[1], b[1], w[0], sum[1], w[1]); 
FA f3(a[2], b[2], w[1], sum[2], w[2]); 
FA f4(a[3], b[3], w[2], sum[3], w[3]); 
FA f5(a[4], b[4], w[3], sum[4], w[4]); 
FA f6(a[5], b[5], w[4], sum[5], w[5]); 
FA f7(a[6], b[6], w[5], sum[6], w[6]);
FA f8(a[7], b[7], w[6], sum[7], carry);
Endmodule
```
### OUTPUT:
![image](https://github.com/sowmithraramesh/VLSI-LAB-EXP-1/assets/166893766/a6b76bf7-bda6-4356-be00-9452b1edcb10)

## RESULT:
      Thus, the logic gates and 4 Bit of Adder and Subtractor are Implemented and simulated successfully.

