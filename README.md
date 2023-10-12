# RISCV_based_myth
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

</details>
