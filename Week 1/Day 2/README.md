

---

````markdown
# Week 1 - Day 2

## 1. Library Files (`.lib`)

A `.lib` file is a **cell library file** used during synthesis.  
It contains information about:
- Standard cells and their different combinations
- Features such as leakage power, voltage (V), current (I), and delay

### Command to Open `.lib` File:
```bash
gedit path/to/library.lib
````
```markdown
![dot lib](images/dot_lib.png)
```
---

## 2. Hierarchical vs Flat Synthesis

* **Hierarchical Synthesis**

  * Maintains the module hierarchy of the design.
  * Easier to understand and debug.
  * Preferred when multiple instances of the same module are used.

* **Flat Synthesis**

  * Flattens the hierarchy into a single module.
  * May optimize better, but harder to debug.

---

## 3. Hierarchical Synthesis Example

### Commands:

```bash
gedit multiple_modules.v
![multiple module code](images/multiple_module_code.png)
yosys
read_liberty -lib path/to/library.lib
read_verilog multiple_modules.v
synth -top multiple_modules
abc -liberty path/to/library.lib
show
```


```markdown
![synth output](images/multiple_module_u12.png)
```

Generate netlist:

```bash
write_verilog multiple_modules_hier.v
!gedit multiple_modules_hier.v
```


```markdown
![Hierarchical Netlist File](images/netlist_multiple_module_hierv.png)
```

---

## 4. Flat Synthesis Example

```bash
read_verilog multiple_modules.v
synth -top multiple_modules
abc -liberty path/to/library.lib
flatten
show
```


```markdown
![synth Flat](images/mm_flatten_show.png)
```

---

## 5. Submodule Level Synthesis

### Why?

* Useful when we have multiple instances of the same module.
* Makes massive designs easier to handle.

### Commands:

```bash
yosys
read_liberty -lib path/to/library.lib
read_verilog sub_module1.v
abc -liberty path/to/library.lib
show
```



```markdown
![ Synth-Submodule ](images/mm_submodule1.png)
```

---

## 6. Various Flip-Flop Coding Styles

### Why Do We Need Flops?

* Pure combinational circuits create glitches.
* A **flip-flop** stores values and avoids glitches.

If not initialized → circuit may evaluate to garbage.
Hence, we use **set** or **reset** signals.

* **Asynchronous reset** → reset occurs immediately, independent of clock.
* **Synchronous reset** → reset occurs with the clock edge.

---

### Example 1: D Flip-Flop with Asynchronous Reset

```bash
iverilog dff_asyncres.v tb_dff_asyncres.v
./a.out
gtkwave tb_dff_asyncres.vcd
```


```markdown
![DFF Async Reset Waveform](images/tb_dff_asyncres.png)
```

Synthesis:

```bash
yosys
read_liberty -lib path/to/library.lib
read_verilog dff_asyncres.v
synth -top dff_asyncres
dfflibmap -liberty path/to/library.lib
abc -liberty path/to/library.lib
show
```


```markdown
![DFF Async Reset Synth](images/dsynth_dff_asyncres.png)
```

---

### Example 2: D Flip-Flop with Asynchronous Set

```bash
iverilog dff_async_set.v tb_dff_async_set.v
./a.out
gtkwave tb_dff_async_set.vcd
```


```markdown
![DFF Async Set Waveform](images/tb_dff_async_set.png)
```

Synthesis:

```bash
yosys
read_liberty -lib path/to/library.lib
read_verilog dff_async_set.v
synth -top dff_async_set
dfflibmap -liberty path/to/library.lib
abc -liberty path/to/library.lib
show
```


```markdown
![DFF Async Set Netlist](images/synth_dff-async_set.png)
```

---

### Example 3: D Flip-Flop with Synchronous Reset

```bash
iverilog dff_syncres.v tb_dff_syncres.v
./a.out
gtkwave tb_dff_syncres.vcd
```



```markdown
![DFF Sync Reset Waveform](images/tb_dff_syncres.png)
```

Synthesis:

```bash
yosys
read_liberty -lib path/to/library.lib
read_verilog dff_syncres.v
synth -top dff_syncres
dfflibmap -liberty path/to/library.lib
abc -liberty path/to/library.lib
show
```



```markdown
![DFF Sync Reset Netlist](images/synth_dff_syncres.png)
```

---




