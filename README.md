

-----

# 🚀 The Silicon Logbook: My RISC-V Tapeout Adventure



Welcome! This is my personal logbook for the **RISC-V Reference SoC Tapeout Program**, an incredible initiative by VSD to design a System-on-Chip from scratch. I'll be documenting my week-by-week progress, challenges, and key learnings here.

-----

## 📅 The Foundation Week: Setting Up the Workbench

This first week was all about preparation—building the digital workbench where all the magic happens. I focused on setting up my Ubuntu environment and installing the complete open-source EDA toolchain.

### **My Learning Highlights**

  - **A Unified Workflow:** I learned that each tool (Yosys, Iverilog, GTKWave) is a specialized part of a larger, unified flow that takes an idea from concept to reality.
  - **The Power of the Terminal:** I gained confidence using commands like `git`, `cp`, `mkdir`, and `nano`, which are fundamental for professional VLSI work.
  - **Solving Dependencies:** I successfully navigated dependency hell, learning how to use `sudo apt-get install` and compile from source to get everything working perfectly.

### **My Toolset & Their Superpowers**

| Tool | My Impression |
|:---|:---|
| **Yosys** | The architect. It takes my RTL blueprints and builds the logical structure of my chip. |
| **Iverilog** | The debugger. It lets me run test simulations to catch any errors in my Verilog code early on. |
| **GTKWave** | The detective. It visualizes my simulation results, helping me find bugs that a simple text log would miss. |
| **OpenLane** | The builder. It automates the entire physical design process, from placing components to connecting wires. |
| **Magic VLSI** | The artist. It's the final stop for fine-tuning the physical layout before it's ready for fabrication. |

### **Proof of Concept: Verifying My Tools**

\<div align="center"\>
\<img src="[https://raw.githubusercontent.com/HarshiniS05/RISC-V\_Tapeout/main/Week%201/images/yosys.png](https://raw.githubusercontent.com/HarshiniS05/RISC-V_Tapeout/main/Week%201/images/yosys.png)" width="300" alt="Yosys Version Check"\>
\<img src="[https://raw.githubusercontent.com/HarshiniS05/RISC-V\_Tapeout/main/Week%201/images/iverilog.png](https://raw.githubusercontent.com/HarshiniS05/RISC-V_Tapeout/main/Week%201/images/iverilog.png)" width="300" alt="Iverilog Version Check"\>
\<img src="[https://raw.githubusercontent.com/HarshiniS05/RISC-V\_Tapeout/main/Week%201/images/gtkwave.png](https://raw.githubusercontent.com/HarshiniS05/RISC-V_Tapeout/main/Week%201/images/gtkwave.png)" width="300" alt="GTKWave Launch"\>
\<img src="[https://raw.githubusercontent.com/HarshiniS05/RISC-V\_Tapeout/main/Week%201/images/ngspice.png](https://raw.githubusercontent.com/HarshiniS05/RISC-V_Tapeout/main/Week%201/images/ngspice.png)" width="300" alt="Ngspice Version Check"\>
\<img src="[https://raw.githubusercontent.com/HarshiniS05/RISC-V\_Tapeout/main/Week%201/images/magic.png](https://raw.githubusercontent.com/HarshiniS05/RISC-V_Tapeout/main/Week%201/images/magic.png)" width="300" alt="Magic GUI"\>
\</div\>

-----

## 💡 What's Next?

\<div align="center"\>

\<img src="[https://via.placeholder.com/150x50.png?text=Week%201%20Task](https://via.placeholder.com/150x50.png?text=Week%201%20Task)" alt="Week 1 task placeholder"\>

\<br\>
I'm excited to dive into the next phase: **RTL design\!** Follow my journey as I transform my first idea into a tangible design.

\</div\>
