# Building a RISCV Core
# TABLE OF CONTENTS
## DAY 1
**Digital Logic with TL-Verilog and Makerchip**  
+ [Combinational Logic in TL-Verilog using Makerchip](#combinational-logic-in-tl-verilog-using-makerchip)
+ [Sequential Logic](#sequential-logic)
+ [Pipelined Logic](#pipelined-logic)
+ [Validity](#validity)

## DAY 2
**Basic RISC-V CPU Microarchitecture**
+ [Introduction](#introduction)
+ [Fetch and Decode](#fetch-and-decode)
+ [RISCV Control Logic](#riscv-control-logic)

## DAY 3
**Complete Pipelined RISC-V CPU Micro-architecture**
+ [Pipelining the CPU](#pipelining-the-cpu)
+ [Solutions to Pipeline Hazards](#solutions-to-pipeline-hazards)
+ [Load/Store Instructions and Completing RISC-V CPU](#load/store-instructions-and-completing-risc-v-cpu)

# Day-1
## Combinational Logic in TL-Verilog using Makerchip
<details>
<summary> Introduction </summary>

+ **Logic Gates**
  
  Logic gates are fundamental building blocks of digital circuits and are used to perform logical operations on binary numbers. They manipulate binary information, where 0 represents false or low voltage, and 1 represents true or high voltage.

<p align="center">
<img width="505" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/dc4c7ced-363f-4712-9ffd-d52da2a217bf">
</p>
<p align="center">
  Fig 1.
</p>

+ **Boolean Operation**

  Boolean operations are fundamental operations in Boolean algebra, a mathematical structure dealing with variables that can take on one of two values, typically denoted as true (1) and false (0).

<p align="center">
<img width="344" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/6d87e1de-cd86-4708-89e5-d8f14c84c5de">
</p>
<p align="center">
  Fig 2.
</p>

+ **Basic Mux Implementation**

   A 2:1 multiplexer (also known as a 2-to-1 mux) is a digital circuit that selects one of two input data lines and directs it to a single output line based on a control signal. The control signal determines which of the two input lines is transmitted to the output.

<p align="center">
<img width="167" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/5d858058-d4b0-4e6e-ad53-d402aab85f7c">
</p>
<p align="center">
  Fig 3.
</p>

``` v
assign f = s ? x1 : x2;
```

+ **Chaining Ternary Operator**

<p align="center">
<img width="151" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/c478b402-a4d2-4bd9-b883-c25bd5c58197">
<img width="157" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/2682bfab-f2b8-4c4a-a90f-e6db6f6c4ac2">
</p>
<p align="center">
  Fig 4.
</p>

```v
assign f = sel[0] ? a : (sel[1] ? b : (sel[2] ? c : d)) ;
```

</details>

<details>
<summary> Makerchip Platform </summary>

+ Go to http://makerchip.com/
+ Click `IDE`
+ Open `Tutorials` then `Validity Tutorial`
+ Click `Load Pythogorean Example`
+ Split planes and move tabs.
+ Zoom/pan in Diagram with mouse wheel and drag.
+ Zoom waveform with `Zoom In` button.
+ Click `$bb_sq` in waveform to highlight in the diagram.

<p align="center">
<img width="960" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/351ab7e6-940b-47c4-9a06-d687d99147f3">
</p>
<p align="center">
  Fig 5.
</p>

</details>

<details>
<summary> Labs </summary>

**Inverter**
+ Open `Examples`(under `Tutorials`).
+ Load `Makerchip Default Template`.
+ Make an inverter.
+ On line 16, in place of `//..` , type `$out = ! $in1;` (preserve 3-space indentation, no tabs).
+ Compile (`E` menu).

<p align="center">
<img width="960" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/afa6bd69-0e70-4ca6-b5a0-4e5d1a5b12fd">
</p>
<p align="center">
  Fig 6.
</p>

  + There was no need to declare $out and $in1 unlike verilog, and no need to assign $in1 . Random stimulus is generated and a warning is produced.


**OR**
+  On line 16, in place of `//..` , type
  ```v
  $out = $in1 | $in2;
  ```

<p align="center">
<img width="959" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/f6cacef7-f094-4e85-950c-2f8c52896250">
</p>
<p align="center">
  Fig 7.
</p>

**Vectors**
+ Arithmetic operations operate on vectors as binary numbers.
+  On line 16, in place of `//..` , type

 ```v
  $out[4:0] = $in1[3:0] + $in2[3:0];
```

+  `$out[4:0]` creates a vecot of 5 bits.

<p align="center">
<img width="959" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/e7f72dc9-45d7-41b2-8194-1846c454065b">
</p>
<p align="center">
  Fig 8.
</p>

**MUX**
+ ```v
  $out = $sel ? $in1 : $in2;
  ```

<p align="center">
<img width="959" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/87170d58-c4d6-4a59-9f4c-d23d9812698d">
</p>
<p align="center">
  Fig 9.
</p>

+ Modified the mux to operate on vectors.
   - ```v
     $out[7:0] = $sel ? $in1[7:0] : $in2[7:0];
     ```

<p align="center">
<img width="959" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/f32f865a-3f6e-4f32-82c2-ca3af28b6c7e">
</p>
<p align="center">
  Fig 10.
</p>

**Combinational Calculator**

<p align="center">
  <img width="308" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/c28c7768-d70f-4bb0-8bc4-e96a78267add">
</p>
<p align="center">
  Fig 11.
</p>

```v
$reset = *reset;
$val1[31:0] = $rand1[3:0];
$val2[31:0] = $rand2[3:0];
$sum[31:0] = $val1[31:0] + $val2[31:0];
$diff[31:0] = $val1[31:0] - $val2[31:0];
$prod[31:0] = $val1[31:0] * $val2[31:0];
$quot[31:0] = $val1[31:0] / $val2[31:0];
$out[31:0] = $op[1] ? ($op[0] ? $quot : $prod)
                    : ($op[0] ? $diff : $sum);
```

<p align="center">
<img width="960" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/b085c8d7-b712-4625-80bf-c9d2bbdc93c0">
</p>
<p align="center">
  Fig 12.
</p>

</details>

## Sequential Logic
<details>
<summary> Introduction </summary>

**Sequential Logic**
+ Sequential logic is sequenced by a clock signal.
+ A D-FF transitions next state to current state on a rising clock edge.
+ The circuit is constructed to enter a known state in response to a reset signal.

<p align="center">
<img width="265" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/b4e2e060-11f2-4d37-92a1-f0118c97f10d">
</p>
<p align="center">
  Fig 1.
</p>

**Values in Verilog**
<p align="center">
  <img width="281" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/e220d1be-1f0f-4cd2-ae27-6a12e73c77ab">
</p>
<p align="center">
  Fig 2.
</p>

+ Simulator configuration :
  - will zero-extend or truncate when widths are mismatched (without warning).
  - uses 2-state simulation (no X's)
</details>

<details>
<summary> Labs </summary>

**Fibonacci Series-Reset**

+ Next value is the sum of previous two numbers: 1, 1, 2, 3, 5, 8, ...
<p align="center">
<img width="247" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/d3998208-dfb3-4375-ab65-3abc633819ac">
</p>
<p align="center">
Fig 3.
</p>

+ ```v
  $num[31:0] = $reset ? 1 : (>>1$num + >>2$num);
  ```

<p align="center">
<img width="959" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/1aeae6a6-4ff7-45c0-8897-b110e5b30c57">
</p>
<p align="center">
Fig 4.
</p>

**Counter**

+ Designed a free running counter.

<p align="center">
<img width="143" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/20c5e180-cb88-4a52-9bfd-f45a8e4f4033">
</p>
<p align="center">
  Fig 5.
</p>

+ ```v
     $cnt[31:0] = $reset ? 0 : (1 + >>1$cnt);
  ```

<p align="center">
<img width="960" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/7f492f6d-24aa-48e6-8a37-a2836264f251">
</p>
<p align="center">
  Fig 6.
</p>

**Sequential Calculator**

<p align="center">
<img width="314" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/b1c50abb-e7e8-4f01-8973-093a02c26cbe">
</p>
<p align="center">
  Fig 7.
</p>

+ ```v
   $reset = *reset;
   $val2[31:0] = $rand2[3:0]; 
   $val1[31:0] = >>1$out[31:0];
   $sum[31:0] = $val1[31:0] + $val2[31:0];
   $diff[31:0] = $val1[31:0] - $val2[31:0];
   $prod[31:0] = $val1[31:0] * $val2[31:0];
   $quot[31:0] = $val1[31:0] / $val2[31:0];
   $out[31:0] = $reset ? 32'b0 :
                ($op[1] ? ($op[0] ? $quot : $prod)
                        : ($op[0]? $diff : $sum));
  ```

<p align="center">
<img width="960" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/5576c9d8-d46e-407a-8473-b2027fe06cee">
</p>
<p align="center">
  Fig 8.
</p>

<p align="center">
<img width="540" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/e2b63305-29bf-41a6-8073-3ac5b504f684">
</p>
<p align="center">
  Fig 9.
</p>

</details>

## Pipelined Logic
<details>
<summary> Introduction </summary>

**Pythagoras's Theorem**

<p align="center">
  <img width="151" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/72828588-2914-46a1-9cc6-22e36ab47151">
</p>
<p align="center">
  Fig 1.
</p>

+ Computation cannot be done in a single cycle, hence we distribute the calculation over 3 cycles.
<p align="center">
  <img width="298" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/d03e696c-fd46-446b-9c44-995806260706">
</p>
<p align="center">
  Fig 2.
</p>

+ TL Verilog gives us the ability to model this in what we called as **timing abstract** representation.
<p align="center">
<img width="284" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/33ed466c-9a22-4411-bb0b-eb6761cc1157">
</p>
<p align="center">
  Fig 3.
</p>

```v
|calc
         @1
            $aa_sq[7:0] = $aa[3:0] ** 2;
            $bb_sq[7:0] = $bb[3:0] ** 2;
         @2
            $cc_sq[8:0] = $aa_sq + $bb_sq;
         @3
            $cc[4:0] = sqrt($cc_sq);
```

**Retiming**
```v
|calc
         @0
            $aa_sq[7:0] = $aa[3:0] ** 2;
         @1 
            $bb_sq[7:0] = $bb[3:0] ** 2;
         @2
            $cc_sq[8:0] = $aa_sq + $bb_sq;
         @4
            $cc[4:0] = sqrt($cc_sq);
```
<p align="center">
  <img width="332" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/3f1d17b0-8ba2-44aa-a4b1-80e2c32e19b3">
</p>
<p align="center">
  Fig 4.
</p>

+ There will be no impact on behavior.

<p align="center">
  <img width="960" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/f4c22366-262d-4241-8dec-c428dc4d974d">
</p>
<p align="center">
  Fig 5. Without pipeline
</p>

<p align="center">
  <img width="959" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/4a53fc38-ab04-4ea0-a3d5-3e74f20bc601">
</p>
<p align="center">
  Fig 6. With pipeline
</p>

**Identifiers and Types**
+ Type of an identifier determined by symbol prefix and case/delimitation style.
<p align="center">
  <img width="158" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/8d4d6c1f-a82a-4ef5-adf8-1b40f7bad737">
</p>
<p align="center">
  Fig 7.
</p>

+ First token must start with two alpha characters.
  - $lower_case : pipe signal
  - $CamelCase : state signal ( Pascal case)
  - $UPPER_CASE : keyword signal
+ Numbers end tokens (after alphas)
  - $base64_value : good
  - $bad_value_5 : bad
+ Numeric identifiers
  - `>>1` : ahead by 1

</details>

<details>
<summary> Labs </summary> 

+ Example
  ```v
  |comp
      
      @1
         $err1 = $bad_input || $illegal_op;
      @3
         $err2 = $err1 || $over_flow;
      @6
         $err3 = $div_by_zero || $err2;
  ```
<p align="center">
  <img width="960" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/3f3cdbc3-39f3-4cf4-aab8-927b48c39cca">
</p>
<p align="center">
  Fig 8.
</p>

+ Counter and Calculator in pipeline

<p align="center">
  <img width="298" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/96837410-4d83-44f5-86c2-f9ceecfc6568">
</p>
<p align="center">
  Fig 9.
</p>

```v
|calc
      @0
         $reset = *reset;
      @1
         $val2[31:0] = $rand2[3:0];
         $val1[31:0] = (>>1$out[31:0]);
         $sum[31:0] = $val1[31:0] + $val2[31:0];
         $diff[31:0] = $val1[31:0] - $val2[31:0];
         $prod[31:0] = $val1[31:0] * $val2[31:0];
         $quot[31:0] = $val1[31:0] / $val2[31:0];
         $out[31:0] = $reset ? 32'b0 :
                      ($op[1] ? ($op[0] ? $quot : $prod)
                              : ($op[0]? $diff : $sum));
         $cnt[31:0] = $reset ? 0 : (1 + >>1$cnt);
```

<p align="center">
<img width="960" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/8e2a534d-fe0d-43a6-97b6-139bc5a41504">
<img width="503" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/1d0f1af7-8ae3-4986-85f1-43b0c19bb772">
</p>
<p align="center">
  Fig 10.
</p>

+ 2-Cycle Calculator
<p align="center">
  <img width="292" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/52da0bab-1d7d-4264-af5a-481c00d26757">
</p>
<p align="center">
  Fig 11.
</p>

```v
|calc 
      @0
         $reset = *reset;
      @1  
         $val1[31:0] = (>>2$out[31:0]);
         $val2[31:0] = $rand2[3:0];
         $sum[31:0] = $val1[31:0] + $val2[31:0];
         $diff[31:0] = $val1[31:0] - $val2[31:0];
         $prod[31:0] = $val1[31:0] * $val2[31:0];
         $quot[31:0] = $val1[31:0] / $val2[31:0];
         $cnt[0] = $reset ? 0 : (1 + >>1$cnt);
      @2
         $valid[0] = $cnt;
         $rst = ~$valid[0] || $reset;
         $out[31:0] = $rst ? 32'b0 :
                      ($op[1] ? ($op[0] ? $quot : $prod)
                              : ($op[0]? $diff : $sum));
```
<p align="center">
<img width="960" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/4b2c78b6-a08b-4195-9bf5-c1ec1799d531">
<img width="476" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/968dc248-1c0c-4d45-a990-32023ff2ab15">
</p>
<p align="center">
  Fig 12.
</p>

</details>

## Validity
<details>
<summary> Introduction </summary> 

+ Validity provides:
  - Easier debug
  - Cleaner design
  - Better error checking
  - Automated clock gating
 
+ Clock gating
  - Clock signals are distributed to every flip flop. CLocks toggle twice per cycle, which consumes power.
  - CLock gating avoids toggling clock signals.
  - TL-verilog can produce fine-grained gating (or enables).
  
</details>

<details>
<summary> Labs </summary>  

+ Distance accumulator

<p align="center">
<img width="341" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/6268ea4f-02f4-44ea-ad0a-00c3bcc10221">
</p>
<p align="center">
  Fig 1.
</p>

```v
|calc
      @1
         $reset = *reset;
      ?$valid
         @1
            $aa_sq[31:0] = $aa[3:0] ** 2;
            $bb_sq[31:0] = $bb[3:0] ** 2;
         @2
            $cc_sq[31:0] = $aa_sq + $bb_sq;
         @3
            $cc[31:0] = sqrt($cc_sq);
      @4
         $tot_dist[63:0] = 
                   $reset ? '0 :
                   $valid ? >>1$tot_dist + $cc :
                            >>1$tot_dist;
```

<p align="center">
  <img width="960" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/7c034523-0164-4d80-808c-a59ae8218355">
</p>
<p align="center">
  Fig 2.
</p>

+ 2-Cycle Calculator with Validity

<p align="center">
  <img width="297" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/4fafe266-cf7c-4bc9-bf16-c145fcc662b2">
</p>
<p align="center">
  Fig 3.
</p>

```v
|calc
      @0
         $reset = *reset;
      @1
         $valid = $reset ? 1'b0 : >>1$valid + 1'b1;
         $val2[31:0] = $rand2[3:0];
         $val1[31:0] = >>2$out;
         $reset_or_valid = $valid || $reset;
      ?$reset_or_valid
         @1
            $sum[31:0] = $val1[31:0] + $val2[31:0];
            $diff[31:0] = $val1[31:0] - $val2[31:0];
            $prod[31:0] = $val1[31:0] * $val2[31:0];
            $quot[31:0] = $val1[31:0] / $val2[31:0];
         @2 
            $out[31:0] = $reset ? 32'b0 : 
                        ($op[1:0] == 2'b00) ? $sum :
                        ($op[1:0] == 2'b01) ? $diff :
                        ($op[1:0] == 2'b10) ? $prod : $quot;
```

<p align="center">
<img width="956" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/442cb8a9-6c62-4c0b-a27a-f367b3ecff19">
<img width="830" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/5eb1d3ca-ca0d-4563-af38-dc2a02bc587f">
</p>
<p align="center">
Fig 4.
</p>

+ Calculator with Single-Value Memory

<p align="center">
  <img width="323" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/81bbd477-b907-40f9-8d03-4582c8c7459f">
</p>
<p align="center">
  Fig 5.
</p>

```v
 |calc
      @0
         $reset = *reset;
      @1
         $valid = $reset ? 1'b0 : >>1$valid + 1'b1;
         $val2[31:0] = $rand2[3:0];
         $val1[31:0] = >>2$out;
         $reset_or_valid = $valid || $reset;
      ?$reset_or_valid
         @1
            $sum[31:0] = $val1[31:0] + $val2[31:0];
            $diff[31:0] = $val1[31:0] - $val2[31:0];
            $prod[31:0] = $val1[31:0] * $val2[31:0];
            $quot[31:0] = $val1[31:0] / $val2[31:0];
         @2 
            $mem[31:0] = $reset ? 32'b0 : 
                         ($op[2:0] == 3'b101) ? $val1 :
                                              >>2$mem;
            $out[31:0] = $reset ? 32'b0 : 
                        ($op[2:0] == 3'b000) ? $sum :
                        ($op[2:0] == 3'b001) ? $diff :
                        ($op[2:0] == 3'b010) ? $prod : 
                        ($op[2:0] == 3'b011) ? $quot : 
                        ($op[2:0] == 3'b100) ? >>2$mem : >>2$out;
```

<p align="center">
<img width="959" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/7d5e4605-d058-45e6-82d1-15f8565c29f2">
<img width="785" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/d2827a11-216d-4e3e-a376-ca69b265b5a1">
</p>
<p align="center">
  Fig 6.
</p>

</details>

<details>
<summary> Hierarchy </summary>

<p align="center">
  <img width="381" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/3154b7a2-b8f3-4173-98f3-f06db688fc1e">
</p>
<p align="center">
  Fig 7.
</p>

<p align="center">
  <img width="959" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/8af0e2ff-58fd-443a-bb89-5c245cf057ff">
</p>
<p align="center">
  Fig 8.
</p>

</details>

# Day-2
## Introduction
<details>
<summary> Micro-architecture of Single Cycle RISC-V CPU </summary>

</details>

## Fetch and Decode
<details>
<summary> Implementation Plan </summary> 

<p align="center">
<img width="436" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/641526e6-4ccd-4dd9-ba7a-c61c4aeab0cc">
</p>
<p align="center">
  Fig 1.
</p>

</details>

<details>
<summary> Labs </summary>

+ Lab for PC

```v
|cpu
      @0
         $reset = *reset;
         $pc[31:0] = >>1$reset ? 32'b0 :
                                 >>1$pc + 32'd4;
```

<p align="center">
<img width="960" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/4bcc36c3-6b4f-475d-8ef9-0970dd2e949c">
</p>
<p align="center">
  Fig 2.
</p>

+ Lab for Insstruction Fetch Logic

```v
|cpu
      @0
         $reset = *reset;
         $pc[31:0] = >>1$reset ? 32'b0 :
                                 >>1$pc + 32'd4;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         $imem_rd_en = !$reset;
      /imem[7:0]
         @1
            $instr[31:0] = *instrs\[#imem\];
      ?$imem_rd_en
         @1
            $imem_rd_data[31:0] = /imem[$imem_rd_addr]$instr;
      @1   
         $instr[31:0] = $imem_rd_data[31:0];
```

<p align="center">
<img width="959" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/60641804-d2f2-44dc-91b3-5e48aaea6b56">
  <img width="939" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/8dec92ae-607d-4b1a-92e1-dc256d8b61dc">
</p>
<p align="center">
  Fig 3.
</p>

+ Lab for Instruction Decode

<p align="center">
  <img width="515" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/3382ad8a-c171-4511-acfc-750e92559fef">
  <img width="465" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/1e7308f0-6ceb-4b9f-ad61-f43fe0893259">
  <img width="457" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/4fee566e-2884-4286-bcb6-cf79db7b16f0">
</p>
<p align="center">
  Fig 4.
</p>

```v
|cpu
      @0
         $reset = *reset;
         $pc[31:0] = >>1$reset ? 32'b0 :
                                 >>1$pc + 32'd4;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         $imem_rd_en = !$reset;
      /imem[7:0]
         @1
            $instr[31:0] = *instrs\[#imem\];
      ?$imem_rd_en
         @1
            $imem_rd_data[31:0] = /imem[$imem_rd_addr]$instr;
      @1   
         $instr[31:0] = $imem_rd_data[31:0];
         $is_b_instr = $instr[6:2] ==? 5'b11000;
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                          $instr[6:2] ==? 5'b011x0 ||
                          $instr[6:2] ==? 5'b10100;
         $is_j_instr = $instr[6:2] ==? 5'b11011;
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                            $instr[6:2] ==? 5'b001x0 ||
                            $instr[6:2] ==? 5'b11001;
         $is_u_instr = $instr[6:2] ==? 5'b0x101;
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         $rs1[4:0] = $instr[19:15];
         $rs2[4:0] = $instr[24:20];
         $rd[4:0] = $instr[11:7];
         $opcode[6:0] = $instr[6:0];
         $funct7[6:0] = $instr[31:25];
         $funct3[2:0] = $instr[14:12];
         $imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                         $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                         $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0} :
                         $is_u_instr ? {$instr[31:12], 12'b0} :
                         $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                                     32'b0;
```
<p align="center">
  <img width="960" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/c2759d98-9eee-457e-8114-6b7fbf1079a6">
<img width="960" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/03f41240-b9c3-4235-ac98-8a1fea97e651">
</p>
<p align="center">
  Fig 5.
</p>

+ Lab for Instruction Decode with Validity

```v
|cpu
      @0
         $reset = *reset;
         $pc[31:0] = >>1$reset ? 32'b0 :
                                 >>1$pc + 32'd4;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         $imem_rd_en = !$reset;
      /imem[7:0]
         @1
            $instr[31:0] = *instrs\[#imem\];
      ?$imem_rd_en
         @1
            $imem_rd_data[31:0] = /imem[$imem_rd_addr]$instr;
      @1   
         $instr[31:0] = $imem_rd_data[31:0];
         $is_b_instr = $instr[6:2] ==? 5'b11000;
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                          $instr[6:2] ==? 5'b011x0 ||
                          $instr[6:2] ==? 5'b10100;
         $is_j_instr = $instr[6:2] ==? 5'b11011;
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                            $instr[6:2] ==? 5'b001x0 ||
                            $instr[6:2] ==? 5'b11001;
         $is_u_instr = $instr[6:2] ==? 5'b0x101;
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         $rs1_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         $rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         $funct3_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $funct7_valid = $is_r_instr;
         $imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                         $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                         $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0} :
                         $is_u_instr ? {$instr[31:12], 12'b0} :
                         $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                                     32'b0;
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
         $opcode[6:0] = $instr[6:0];
```

<p align="center">
<img width="960" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/e3d00438-2e4e-4062-84f7-d35c8211708c">
<img width="960" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/00b680d8-58de-4695-b31e-04f293ee9185">
</p>
<p align="center">
  Fig 6.
</p>

+ Lab to Decode Individual Instruction

<p align="center">
  <img width="328" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/9ac885b0-78de-4cd0-a46a-3a1c77a378ce">
</p>
<p align="center">
  Fig 7.
</p>

```v
|cpu
      @0
         $reset = *reset;
         $pc[31:0] = >>1$reset ? 32'b0 :
                                 >>1$pc + 32'd4;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         $imem_rd_en = !$reset;
      /imem[7:0]
         @1
            $instr[31:0] = *instrs\[#imem\];
      ?$imem_rd_en
         @1
            $imem_rd_data[31:0] = /imem[$imem_rd_addr]$instr;
      @1   
         $instr[31:0] = $imem_rd_data[31:0];
         $is_b_instr = $instr[6:2] ==? 5'b11000;
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                          $instr[6:2] ==? 5'b011x0 ||
                          $instr[6:2] ==? 5'b10100;
         $is_j_instr = $instr[6:2] ==? 5'b11011;
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                            $instr[6:2] ==? 5'b001x0 ||
                            $instr[6:2] ==? 5'b11001;
         $is_u_instr = $instr[6:2] ==? 5'b0x101;
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         $rs1_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         $rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         $funct3_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $funct7_valid = $is_r_instr;
         $imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                         $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                         $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0} :
                         $is_u_instr ? {$instr[31:12], 12'b0} :
                         $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                                     32'b0;
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
         $opcode[6:0] = $instr[6:0];         
         $dec_bits[10:0] = {$funct7[5], $funct3, $opcode};
         $is_bne = $dec_bits ==? 11'bx_001_1100011;
         $is_bltu = $dec_bits ==? 11'bx_110_1100011;
         $is_blt = $dec_bits ==? 11'bx_100_1100011;
         $is_bgeu = $dec_bits ==? 11'bx_111_1100011;
         $is_bge = $dec_bits ==? 11'bx_101_1100011;
         $is_beq = $dec_bits ==? 11'bx_000_1100011;
         $is_addi = $dec_bits ==? 11'bx_000_0010011;
         $is_add = $dec_bits ==? 11'b0_000_0110011;
```

<p align="center">
  <img width="960" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/803be52a-1ea9-4070-8ddd-027344e2ca13">
  <img width="960" alt="image" src="https://github.com/Veda1809/RISCV_based_myth/assets/142098395/718c8298-3bba-4f35-846d-d30e820ac344">
</p>
<p align="center">
  Fig 8.
</p>

</details>
