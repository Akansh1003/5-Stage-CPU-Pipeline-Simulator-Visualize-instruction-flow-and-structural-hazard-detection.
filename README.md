# 5-Stage-CPU-Pipeline-Simulator-Visualize-instruction-flow-and-structural-hazard-detection.
This simulator models a classic 5-stage RISC pipeline: IF (Instruction Fetch), ID (Instruction Decode), EX (Execute), MEM (Memory Access), and WB (Write Back). Its core purpose is to demonstrate how multiple instructions overlap in execution, improving throughput at the cost of complexity.
🖥️ 5-Stage CPU Pipeline Simulator
https://img.shields.io/badge/License-MIT-yellow.svg
https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white
https://img.shields.io/badge/JavaScript-ES6-F7DF1E?logo=javascript&logoColor=black

An interactive, browser-based simulator for a classic 5-stage RISC pipeline (IF → ID → EX → MEM → WB) with real-time visualization of instruction flow, structural hazard detection, and resource utilization tracking.

https://via.placeholder.com/800x400?text=5-Stage+Pipeline+Simulator+Screenshot

Live Demo: file:///C:/Users/sriva/Downloads/cpu_pipeline_simulator.html

📚 Table of Contents
Features

Pipeline Stages

Supported Instructions

Quick Start

Hazard Detection

Resource Configuration

Visualization Guide

File Structure

Browser Compatibility

Contributing

License

✨ Features
Category	Capabilities
Pipeline Stages	Full 5-stage: IF, ID, EX, MEM, WB
Instruction Support	R-type (ADD, SUB, MUL, AND, OR, XOR, SLT), Memory (LW, SW), Branch (BEQ, BNE, BLT, BGT)
Hazard Detection	Structural (ALU, MEM, WB, IF bus), Data (RAW with forwarding), Control (branch flush)
Real-time Viz	Pipeline timing diagram, register file state, resource utilization bars
Configurable	ALU units (1-4), Memory ports (1-2), WB ports (1-2)
Preset Programs	Structural hazards demo, mixed hazards, clean pipeline
🔧 Pipeline Stages
text
    ┌─────┐    ┌─────┐    ┌─────┐    ┌──────┐    ┌─────┐
    │ IF  │ → │ ID  │ → │ EX  │ → │ MEM  │ → │ WB  │
    └─────┘    └─────┘    └─────┘    └──────┘    └─────┘
   Fetch     Decode    Execute    Memory      Write
                      (ALU op)    Access      Back
Stage	Color	Description
IF	🔵 Blue	Fetch instruction from memory, increment PC
ID	🟢 Green	Decode instruction, read registers, generate control signals
EX	🟠 Orange	ALU operation (add/sub/mul/logical) or address calculation
MEM	🔴 Pink	Data memory read/write (LW/SW instructions)
WB	🟣 Purple	Write result back to register file
📝 Supported Instructions
R-Type (Register)
text
ADD R1, R2, R3    → R1 = R2 + R3
SUB R1, R2, R3    → R1 = R2 - R3
MUL R1, R2, R3    → R1 = R2 × R3
AND R1, R2, R3    → R1 = R2 & R3
OR  R1, R2, R3    → R1 = R2 | R3
XOR R1, R2, R3    → R1 = R2 ^ R3
SLT R1, R2, R3    → R1 = (R2 < R3) ? 1 : 0
Memory (Load/Store)
text
LW  R1, 0(R2)     → R1 = MEM[R2 + 0]
SW  R1, 4(R2)     → MEM[R2 + 4] = R1
Branch (Control)
text
BEQ R1, R2        → Branch if R1 == R2
BNE R1, R2        → Branch if R1 != R2
BLT R1, R2        → Branch if R1 < R2
BGT R1, R2        → Branch if R1 > R2
🚀 Quick Start
Option 1: Run directly in browser
Save the cpu_pipeline_simulator.html file

Double-click to open in any modern browser

No server or installation required!

Option 2: GitHub Pages
bash
git clone https://github.com/yourusername/5-stage-cpu-pipeline-simulator.git
cd 5-stage-cpu-pipeline-simulator
# Push to GitHub, then enable Pages on main branch
Basic Usage
assembly
# 1. Write your program in the textarea
ADD R1, R2, R3
LW  R7, 0(R1)
LW  R2, 4(R1)
ADD R8, R4, R7

# 2. Click "Load" to compile
# 3. Press "Step" to advance cycle by cycle
# 4. Or "Auto" to run continuously
# 5. Watch the pipeline fill up!
⚠️ Hazard Detection
Types of Hazards Demonstrated
Hazard Type	Detection Example	Simulator Output
Structural (ALU)	3 instructions in EX with only 1 ALU	Structural hazard (ALU): 3 instructions competing
Structural (MEM)	Multiple LW/SW in same cycle	Structural hazard (MEM): 2 memory ops competing
Structural (WB)	2 instructions finishing simultaneously	Structural hazard (WB): 2 writebacks competing
Data (RAW)	ADD R1 → LW R1 in next instruction	Data hazard (EX forwarding): R1 → LW R1, 0(R2)
Load-Use Stall	LW followed by dependent ADD	Data hazard (load-use stall): LW → ADD
Control	Branch instruction in EX	Control hazard: branch resolves → flush IF/ID
Hazard Log Coloring
🟣 Structural — Resource contention

🟠 Data (RAW) — Read-after-write dependency

🟢 Data (forwarded) — Successfully resolved via forwarding

🔴 Control — Branch misprediction (flush)

⚙️ Resource Configuration
Adjust hardware resources in real-time to observe structural hazards:

Resource	Default	Range	Effect on Pipeline
ALU Units	1	1-4	More units = fewer ALU structural hazards
Memory Ports	1	1-2	Affects LW/SW concurrency
WB Ports	1	1-2	Writeback congestion at completion
Try this: Set ALU=1, MEM=1 → run structural hazard preset → watch the pipeline stall!

📊 Visualization Guide
1. Pipeline Timing Diagram
Rows = Instructions, Columns = Cycles

Each cell shows which stage an instruction occupies

stall = pipeline bubble inserted

— = flushed instruction (after branch)

2. Resource Utilization Bars
Shows % of cycles each resource was busy

ALU, Memory, IF bus, WB port

Changes color when resource is contested

3. Register File
8 registers (R0–R7) displayed

Highlighted registers = written during this simulation

Values are symbolic (randomized for memory reads)

4. Hazard Log
Chronological list of detected hazards

Shows cycle number and affected instructions

Color-coded by hazard type

📁 File Structure
text
5-stage-cpu-pipeline-simulator/
│
├── cpu_pipeline_simulator.html    # Single-file application (HTML/CSS/JS)
│
├── README.md                       # This file
├── LICENSE                         # MIT License
│
└── examples/                       # Sample programs (optional)
    ├── structural_hazards.asm
    ├── data_hazards.asm
    └── branch_test.asm
Note: This is a zero-dependency, single-file application — everything runs in the browser!

🌐 Browser Compatibility
Browser	Version	Status
Chrome	90+	✅ Full support
Firefox	88+	✅ Full support
Safari	14+	✅ Full support
Edge	90+	✅ Full support
Opera	75+	✅ Full support
Requires JavaScript enabled. Works offline after first load.

🎯 Preset Programs
Click the preset buttons to load ready-made examples:

Preset	Description	What You'll See
Structural hazards	2 LW instructions + ALU ops	MEM port contention, ALU unit conflicts
All hazards	LW, ADD, BEQ, SW sequence	Load-use stall + branch flush + forwarding
No hazards	R-type instructions only	Smooth pipelining, perfect CPI
🛠️ Technical Details
Pipeline Behavior
Forwarding: EX→EX and MEM→EX forwarding paths implemented

Stalling: Load-use hazards insert 1-cycle stall

Flushing: Branches flush IF/ID stages on resolution

Structural resolution: Stalls the conflicting instruction

Limitations (Educational Focus)
Simplified memory model (no cache)

8 registers for display clarity

Random values for memory reads (demonstration only)

No branch prediction (always flush on taken branch)

🤝 Contributing
Contributions welcome! Here are some enhancement ideas:

Add branch predictor (static/2-bit)

Cache memory simulation (L1 hit/miss)

Performance metrics (CPI, IPC, stall cycles)

Export pipeline trace as CSV/JSON

Dark/light theme toggle (already follows system!)

Add floating-point instructions (FADD, FMUL)

Save/load programs from localStorage

Cycle-by-cycle register value animation

How to contribute:

bash
fork → create branch → make changes → open pull request
📄 License
Distributed under the MIT License. See LICENSE file for details.

🙏 Acknowledgments
Inspired by Computer Organization and Design (Patterson & Hennessy)

5-stage RISC pipeline from MIPS architecture

Built with vanilla HTML/CSS/JS — no frameworks needed

📧 Contact
Author: Akansh
Project Link: https://github.com/Akansh/5-stage-cpu-pipeline-simulator
Issues: Open an issue

Happy pipelining! 🚀

📸 Screenshots
(Add actual screenshots of your simulator here)

text
┌─────────────────────────────────────────────────────────────────┐
│  Controls: [Step] [Auto] [Reset]    Speed: ●━━━━━━━○ 700ms      │
├─────────────────────────────────────────────────────────────────┤
│  Pipeline Timing Diagram                                        │
│  ┌────────┬─────┬─────┬─────┬─────┬─────┐                      │
│  │Instr   │ C1  │ C2  │ C3  │ C4  │ C5  │                      │
│  │ADD R...│ IF  │ ID  │ EX  │ MEM │ WB  │                      │
│  │LW R7...│     │ IF  │ ID  │ EX  │ MEM │                      │
│  │ADD R...│     │     │stall│ ID  │ EX  │                      │
│  └────────┴─────┴─────┴─────┴─────┴─────┘                      │
├─────────────────────────────────────────────────────────────────┤
│  Hazard Log                                                     │
│  C3: Data hazard (load-use stall): LW → ADD                     │
└─────────────────────────────────────────────────────────────────┘
⭐ Star this repository if you find it useful for teaching or learning computer architecture!
