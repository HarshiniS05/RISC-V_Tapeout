
---

# Day 5: Optimization in Synthesis & IF/CASE Constructs

---

## 📌 Introduction

In digital design, **optimization during synthesis** ensures that the RTL is mapped efficiently to hardware while preserving intended functionality.
The way we write RTL using **IF and CASE constructs** has a major impact on the synthesized logic.

---

## 🔹 IF Constructs

### 1. **Priority Logic with IF**

* The `if` statement introduces **priority logic**.
* Example:

  ```verilog
  if (cond1)
      y = a;
  else if (cond2)
      y = b;
  else
      y = c;
  ```

  ➝ This means **cond1 has the highest priority**, then cond2, and finally default.

---

### 2. **Danger / Caution with IF**

* **Incomplete IF statements** can lead to **inferred latches**.
* Latches are not always desired and may cause **timing hazards**.

✅ Example of unintended latch:

```verilog
always @(*) begin
    if (en)
        q = d;    // Missing else → q holds previous value → latch inferred
end
```

---

### 3. **When Latches Are Intended**

* In some designs, like **counters with enable**, latches are intentionally created.
* Example:

```verilog
always @(posedge clk) begin
    if (en)
        count <= count + 1;  
    // if en is 0 → count holds previous value → latch-like behavior
end
```

---

## 🔹 CASE Constructs

### 1. **Usage**

* `case` statements are commonly used inside **always blocks** to select among multiple choices.

Example:

```verilog
always @(*) begin
    case(sel)
        2'b00: y = a;
        2'b01: y = b;
        2'b10: y = c;
        default: y = d;
    endcase
end
```

---

### 2. **Incomplete CASE Statements**

* Missing a **default case** can also create **inferred latches**.
* Good practice: Always include a `default` branch, even if unused.

✅ Example (safe coding style):

```verilog
case(sel)
    2'b00: y = a;
    2'b01: y = b;
    2'b10: y = c;
    default: y = d;   // prevents latch
endcase
```

---
## Examples 
### incomplete if
code:
```verilog
module incomp_if (input i0 , input i1 , input i2 , output reg y);
always @ (*)
begin
	if(i0)
		y <= i1;
end
endmodule
```
![design](images/design_incompif.png)

## simulation:
```
iverilog incomp_if.v tb_incomp_if.v
./a.out
gtkwave tb_incomp_if.vcd
```
![rtl_testbench](images/tb_incompif.png)

##synthesis:
```tcl
yosys
read_liberty -lib ../VLSI/sky130RTLDesignAndSynthesisWorkshop/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog incomp_if.v
synth -top incomp_if
abc -liberty ../VLSI/sky130RTLDesignAndSynthesisWorkshop/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```
![synthesis output](images/synth_incompif.png)


---
### incomplete if2
code:
```verilog
module incomp_if2 (input i0 , input i1 , input i2 , input i3, output reg y);
always @ (*)
begin
	if(i0)
		y <= i1;
	else if (i2)
		y <= i3;

end
endmodule
```
![design](images/design_incompif2.png)

## simulation:
```
iverilog incomp_if2.v tb_incomp_if2.v
./a.out
gtkwave tb_incomp_if2.vcd
```
![rtl_testbench](images/tb_incompif2.png)

##synthesis:
```tcl
yosys
read_liberty -lib ../VLSI/sky130RTLDesignAndSynthesisWorkshop/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog incomp_if2.v
synth -top incomp_if2
abc -liberty ../VLSI/sky130RTLDesignAndSynthesisWorkshop/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```
![synthesis output](images/synth_incompif2.png)

---
### incomp_case
code:
```verilog
module incomp_case (input i0 , input i1 , input i2 , input [1:0] sel, output reg y);
always @ (*)
begin
	case(sel)
		2'b00 : y = i0;
		2'b01 : y = i1;
	endcase
end
endmodule
```
![design](images/design_incompcase.png)

## simulation:
```
iverilog incomp_case.v tb_incomp_case.v
./a.out
gtkwave tb_incomp_if.vcd
```
![rtl_testbench](images/tb_incompcase.png)

##synthesis:
```tcl
yosys
read_liberty -lib ../VLSI/sky130RTLDesignAndSynthesisWorkshop/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog incomp_case.v
synth -top incomp_case
abc -liberty ../VLSI/sky130RTLDesignAndSynthesisWorkshop/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```
![synthesis output](images/synth_incompcase.png)


---

### comp_case
code:
```verilog
module comp_case (input i0 , input i1 , input i2 , input [1:0] sel, output reg y);
always @ (*)
begin
	case(sel)
		2'b00 : y = i0;
		2'b01 : y = i1;
		default : y = i2;
	endcase
end
endmodule
```
![design](images/design_compcase.png)

## simulation:
```
iverilog comp_case.v tb_comp_case.v
./a.out
gtkwave tb_comp_if.vcd
```
![rtl_testbench](images/tb_compcase.png)

##synthesis:
```tcl
yosys
read_liberty -lib ../VLSI/sky130RTLDesignAndSynthesisWorkshop/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog comp_case.v
synth -top comp_case
abc -liberty ../VLSI/sky130RTLDesignAndSynthesisWorkshop/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```
![synthesis output](images/synth_compcase.png)


---

### bad_case
code:
```verilog
module bad_case (input i0 , input i1, input i2, input i3 , input [1:0] sel, output reg y);
always @(*)
begin
	case(sel)
		2'b00: y = i0;
		2'b01: y = i1;
		2'b10: y = i2;
		2'b1?: y = i3; //it cause confusion
		//2'b11: y = i3;
	endcase
end

endmodule
```


## simulation:
```
iverilog bad_case.v tb_bad_case.v
./a.out
gtkwave tb_bad_case.vcd
```
![rtl_testbench](images/tb_badcase.png)

##synthesis:
```tcl
yosys
read_liberty -lib ../VLSI/sky130RTLDesignAndSynthesisWorkshop/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog bad_case.v
synth -top bad_case
abc -liberty ../VLSI/sky130RTLDesignAndSynthesisWorkshop/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```
![synthesis output](images/synth_badcase.png)
---
### partial_case_assign
code:
```verilog
module partial_case_assign (input i0 , input i1 , input i2 , input [1:0] sel, output reg y , output reg x);
always @ (*)
begin
	case(sel)
		2'b00 : begin
			y = i0;
			x = i2;
			end
		2'b01 : y = i1;
		default : begin
		           x = i1;
			   y = i2;
			  end
	endcase
end

```


## simulation:
```
iverilog partial_case_assign.v tb_partial_case_assign.v
./a.out
gtkwave tb_partial_case_assign.vcd
```
![rtl_testbench](images/tb_partialcase.png)

##synthesis:
```tcl
yosys
read_liberty -lib ../VLSI/sky130RTLDesignAndSynthesisWorkshop/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog partial_case_assign.v
synth -top partial_case_assign
abc -liberty ../VLSI/sky130RTLDesignAndSynthesisWorkshop/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```
![synthesis output](images/synth_partialcase.png)


---


